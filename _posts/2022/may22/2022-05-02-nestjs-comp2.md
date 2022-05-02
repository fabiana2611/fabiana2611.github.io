---
layout: post
title:  "NestJS - components part II"
date:   2022-05-02
categories: node
permalink: /:categories/nestjs-advanced
---

<p style="text-align: justify;">This post has some notes and the code I did while studying nestjs. I started those notes in my <a href="https://fabiana2611.github.io/node/nestjs">first post</a> about nestjs with simple use of the components. Now, I am going a step forward to use some components in a different way and use other resources available in nestjs framework. My references are the udemy course <a href="https://www.udemy.com/course/nestjs-the-complete-developers-guide/">NestJS: The Complete Developer's Guide</a> and the <a href="https://docs.nestjs.com/">nest page</a>. The code used in this post you can find inside the <a href="https://github.com/fabiana2611/nestjs2/tree/master/messages-level-3">messages-level-3 project</a>.

<p> The resources will be shown here are:</p>
<ul style="-webkit-column-count: 2; column-count: 2; -moz-column-count: 2;">
  <li><a href="#providers">Providers</a></li>
  <li><a href="#interceptors">Interceptors</a></li>
  <li><a href="#session">Session</a></li>
  <li><a href="#cookie">Cookie</a></li>
  <li><a href="#dynamicmodule">Dynamic Module</a></li>
</ul>

<h3><u id="providers">Providers</u></h3>

<p style="text-align: justify;">This first topic was already shown in the <a href="https://fabiana2611.github.io/node/nestjs#provider">last post</a>. It shows the basic way to use the providers. However, there are <a href="https://docs.nestjs.com/fundamentals/custom-providers">other ways</a> to set them.</p>

<p><b><u>Standard / useClass</u></b></p>

<p>Use the class name inside the provider is the short way make the Nest IoC container handler the instance. </p>

{% highlight ruby %}
# Complete way - same result of the short way
# 'provide' attribute is the token
# 'useClasse' attribute is the class will be instantiate
providers: [
    { provide: MessagesService, useClass: MessagesService },
];
{% endhighlight %}

<p>It is using 'useClass' attribute. It's possible to decide between different classes to be instantiate.</p>

{% highlight ruby %}
providers: [{
  provide: MessagesService,
  useClass:
    process.env.NODE_ENV === 'development'
      ? DevelopmentMessagesService
      : ProductionMessagesService,
  }],
{% endhighlight %}


<p><b><u>useValue</u></b></p>

<p>It can be used when you want give the instance. In this, the instance was created.</p>

{% highlight ruby %}
# 'provide' attribute is the token
# 'useValue' attribute is the instance will be used when find the token
providers: [
    { provide: MessagesService, useValue: mockMessages },
];
{% endhighlight %}

<p><b><u>Non-class-based provider tokens</u></b></p>

<p>In this case, the 'provide' attribute can be used with a string. To use it by IoC is necessary use the @Inject inside the constructor and do the reference.</p>

{% highlight ruby %}
# Inside the module declaration
providers: [
    { provide: 'CONNECTION', useValue: connection, },
  ],

# Contructor who use it
constructor(@Inject('CONNECTION') connection: Connection) {}
{% endhighlight %}


<p><b><u>useFactory</u></b></p>

<p>It can be used to create providers dynamically. The function that define the useFactory can be an <a href="https://docs.nestjs.com/fundamentals/async-providers">asynchronous function</a>.</p>

{% highlight ruby %}
providers: [
  {
    provide: 'CONNECTION',
    useFactory: (connection: Connection) => {
        return new DatabaseConnection(connection);
    },
  },
],
{% endhighlight %}


<p><b><u>exports</u></b></p>

<p style="text-align: justify;">The export attribute is used when you want the resource from that module be available by other module. It can be a service or controller (e.g) from the current module, or even some resource (service, module, etc) you import to be used by the current module but you want it be visible for who import the current module.</p>

<p style="text-align: justify;">So, considering we have the first module 'messages' and the second module 'auth'. Messages module will have access to the auth resource when the service is declared in the @Module decorator in AuthModule inside the export and in import attribute inside the messages module.</p>

{% highlight ruby %}
# AUTH
@Injectable()
export class AuthService {...}

@Module({
  providers: [AuthService],
  exports: [AuthService],
})
export class AuthModule {}

# MESSAGES
@Module({
    imports: [AuthModule],
    providers: [MessagesService, MessagesRepository],
    controllers: [MessagesController],
})
export class MessagesModule {...}

@Controller('messages')
export class MessagesController {
  constructor(private authService: AuthService) {}

  @Get('/auth/test')
  authTest() {
    this.authService.signin('test@test', '123');
  }  
}

# To test
http://localhost:3001/messages/auth/test    
{% endhighlight %}


<h3><u id="interceptors">Interceptors</u></h3>

<p style="text-align: justify;">In the <a href="https://fabiana2611.github.io/node/nestjs#interceptors">last post</a>, the example shows how to use interceptors. It used the @UseInterceptors decorator from '@nestjs/common'. Let's go forward and create our interceptor.</p>

<p style="text-align: justify;">The example below create  the @Serialize interceptor decorator. Pay attention that the class doesn't have the @Inject but a function. The attribute 'excludeExtraneousValues' print the value in the browser if false and return an empty value if true.

{% highlight ruby %}
# serialize.interceptor.ts
export function Serialize(dto: any) {
  return UseInterceptors(new SerializeInterceptor(dto));
}

export class SerializeInterceptor implements NestInterceptor {
  // make method reusable
  constructor(private dto: any) {}

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('--> Starting my SerializeInterceptor ...');
    return next.handle().pipe(
      map((data: any) => {
        console.log('I am running before response is sent out', data);
        return plainToClass(this.dto, data, {
          excludeExtraneousValues: false,
        });
      }),
    );
  }
}

# The controller
@Serialize(CreateMessageDto)
 @Get('/:id')
 async getMessage(@Param('id') id: string) {...}

{% endhighlight %}

<p style="text-align: justify;">If you need to have an interceptor with a global scope you can declare it inside the module. However, you can choose to use the middleware instead of that because of the order of execution. Middleware executes before the interceptors and Interceptors run after guards. If you need run before the guards you need to create middleware.</p>

{% highlight ruby %}
@Module({
  imports: [AuthModule],
  providers: [MessagesService, MessagesRepository,
     { provide: APP_INTERCEPTOR,  useClass: MessagesInterceptor  }
  ],
  controllers: [MessagesController],
})
export class MessagesModule {...}
{% endhighlight %}

<br />

<h3><u id="session">Session</u></h3>

<p style="text-align: justify;">You can use the <a href="https://docs.nestjs.com/techniques/session">session</a> object to storage information across multiple requests. In a simple example is necessary to have the express-session installed and the main.js configurated.</p>

{% highlight ruby %}
# Command line
$ npm install express-session
$ npm install -D @types/cookie-session

# main.js
import * as session from 'express-session';
// somewhere in your initialization file
app.use(
  session({
    secret: 'my-secret',
    resave: false,
    saveUninitialized: false,
  }),
);

# controller
// #1
@Get('/chats')
async getChat(@Session() session: any) {
  return session.chat;
}

@Get('/chats/:chat')
async setChat(@Param('chat') chat: string, @Session() session: any) {
  session.chat = chat;
}
{% endhighlight %}

<p style="text-align: justify;">To test the session you can test in the browser the ''/chats/:chat' endpoint, which will storage the value in the session, and after that use the endpoint '/chats'. The last endpoint will print for you what you sent previously.</p>

{% highlight ruby %}
### Access endpoint to send the value
GET http://localhost:3001/auth/chats/mynewmessagetosession

HTTP/1.1 200 OK
...
Set-Cookie: connect.sid=s%3AB3A6iFeVckDgWR9CNiuiC3_x04zaWUqF.3GcTJzghp5pINrTGxgeagpnKM%2FyJXzZU%2BVGkF92YdqU; Path=/; HttpOnly

<Response body is empty>

### Access the second endpoint to get the value
GET http://localhost:3001/auth/chats

HTTP/1.1 200 OK
...

mynewmessagetosession
Response file saved.
{% endhighlight %}


<br />
<h3><u id="cookie">Cookie</u></h3>

<p style="text-align: justify;">As far as session storage data across requests, <a href="https://docs.nestjs.com/techniques/cookies">cookie</a> storage data in the user's browser.</p>

<p>Following the nestjs documentation, we will use cookie-parser.</p>

{% highlight ruby %}
# Install
$ npm i cookie-parser
$ npm i -D @types/cookie-parser

# main.js
import * as cookieParser from 'cookie-parser';
app.use(cookieParser());

# The controller
@Get()
findAll(@Req() request: Request) {
  console.log('1: ');
  console.log(request.cookies);
  console.log('2: ');
  console.log(request.cookies['cookieKey']);
  console.log('3: ');
  console.log(request.signedCookies);
}

# The result in terminal
1:
{
  'connect.sid': 's:B3A6iFeVckDgWR9CNiuiC3_x04zaWUqF.3GcTJzghp5pINrTGxgeagpnKM/yJXzZU+VGkF92YdqU',
  session: 'eyJjaGF0IjoibmV3Y2hhdCJ9',
  'session.sig': 'IJzDfLNQgZBcda9q3T1zzLPO5yQ'
}
2:
undefined
3:
[Object: null prototype] {}

{% endhighlight %}

<p style="text-align: justify;">An alternative is to use cookie-session. In this case, you cannot use the import in the main.js file. You have to use a variable because of the incompatibility with nestjs.</p>

{% highlight ruby %}
# install
$ npm install cookie-session @types/cookie-session

# Insert this code out side of the bootstrap method
const cookieSession = require('cookie-session');

# Config
app.use(
  cookieSession({
  name: 'session',
  keys: ['asdfasfd'],
  maxAge: 24 * 60 * 60 * 1000 // 24 hours
}),
{% endhighlight %}



<br />
<h3><u id="dynamicmodule">Dynamic Module</u></h3>

<p style="text-align:justify;">Until now, we have seen the modules been declared statically. Just add the service name, for instance, inside the providers. However, there are some scenarios where is necessary to decide between different services, as by environment.</p>

<p style="text-align: justify;">Here is an example of how to choose between two services and use some attributes injected to do the processing. Here is using <a href="https://docs.nestjs.com/fundamentals/dynamic-modules#:~:text=Config%20module%20example-,%23,-We%27ll%20be%20using">config</a> example by environment. </p>

<p style="text-align: justify;">The ConfigureModule is added inside the module will use it. In the example will be MessagesModule. The static method 'register' is created inside the ConfigureModule and pass a parameter to be used in the decisions.<p>

{% highlight ruby %}
@Module({
  imports: [AuthModule, ConfigModule.register({ attribute: 'staging' })],
  providers: [MessagesService, MessagesRepository],
  controllers: [MessagesController],
})
export class MessagesModule {
{% endhighlight %}

<p style="text-align: justify;">Inside the ConfigModule is done the decision about which class will be used. Also, it's create the provide 'fileProvide' be used for some class. In this example, production class will use it.</p>

{% highlight ruby %}
#config.module
@Module({})
export class ConfigModule {
  static register(param: { attribute: string }): DynamicModule {
    const classProvide =
      param.attribute === 'development'
        ? ConfigDevelopmentService
        : ConfigProductionService;

    const fileProvide = {
      provide: 'CONFIG_OPTIONS',
      useValue: param,
    };

    return {
      module: ConfigModule,
      providers: [classProvide, fileProvide],
      exports: [classProvide],
    };
  }
}

# config-production.service
@Injectable()
export class ConfigProductionService {
  constructor(@Inject('CONFIG_OPTIONS') private options) {
    console.log('---> Starting ConfigProduction...');

    if (options.attribute === 'production') {
      console.log('---> It is in production environment');
    } else {
      console.log(`---> It is in test environment: ${options.attribute}`);
    }
  }
}
{% endhighlight %}


<h3>Conlusion</h3>

<p style="text-align: justify;">Here we saw more about the components. However, it is an overview yet. The difficult part is using all of this in a real project. But don't worry. Baby steps.</p>
