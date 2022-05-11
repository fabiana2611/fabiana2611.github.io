---
layout: post
title:  "NestJS - Security"
date:   2022-05-11
categories: node
permalink: /:categories/nestjs-security
---

<p style="text-align: justify;">This post has some notes and the code I did while studying nestjs. I started those notes in my <a href="https://fabiana2611.github.io/node/nestjs">first post</a> about nestjs with simple use of the components and a <a href="https://fabiana2611.github.io/node/nestjs-advanced">second post</a> as a second step how to use the components. Now, I am going a step forward to use some security resources. More detail about it you can see in the <a href="https://docs.nestjs.com/">nestjs page</a>. The code used in this post you can find inside the <a href="https://github.com/fabiana2611/nestjs2/tree/master/messages-level-3">messages-level-3 project</a>.

<p> The components will be shown here are:</p>
<ul style="-webkit-column-count: 2; column-count: 2; -moz-column-count: 2;">
  <li><a href="#authentication">Authentication</a></li>
  <li><a href="#authorization">Authorization</a></li>
  <li><a href="#encryptation">Encryptation</a></li>
  <li><a href="#helmet">Helmet</a></li>
  <li><a href="#cors">CORS</a></li>
  <li><a href="#csrf">CSRF Protection</a></li>
  <li><a href="#ratelimiting">Rate Limiting</a></li>
</ul>


<br />
<h3><u id="authentication">Authentication</u></h3>

<p style="text-align: justify;">The <a href="https://docs.nestjs.com/security/authentication">Authentication</a> is the guarantee you really are who you say you are. One way to make it safe is not only user and password but use token as well. It returns a token to be used in the next requests to validate the user.</p>

<p><em>Authentication (username/password) -> returning a JWTRequest -> JWT (token) -> protected route</em></p>

{% highlight ruby %}
# To install to use passport
$ npm install --save @nestjs/passport passport passport-local
$ npm install --save-dev @types/passport-local
#to use token
$ npm install --save @nestjs/jwt passport-jwt
$ npm install --save @types/passport-jwt

{% endhighlight %}

<p style="text-align: justify;">The token can helps to protect the available routes to an authenticated user. The process can be done using the @AuthGuard, creating a Strategy class to config the process to handle the token, and using the guard over the endpoint. The <a href="https://docs.nestjs.com/security/authentication">NestJS page</a> shows the complete example to use it.</p>

{% highlight ruby %}
# PS: Code from NestJS page
# Strategy
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: jwtConstants.secret,
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, username: payload.username };
  }
}

# Module will use JWT  
@Module({
  imports: [
    UsersModule,
    PassportModule,
    JwtModule.register({
      secret: jwtConstants.secret,
      signOptions: { expiresIn: '60s' },
    }),
  ],
  providers: [AuthService, LocalStrategy, JwtStrategy],
  exports: [AuthService],
})
export class AuthModule {}

@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}

# Controller
@UseGuards(JwtAuthGuard)
@Get('profile')
getProfile(@Request() req) {
  return req.user;
}  
{% endhighlight %}

<p style="text-align: justify;">However, it's possible make it global to all endpoints. For that, it's necessary define on the main module, improve the guard and create a decorator to be used in the endpoints that should skip the authentication.</p>

{% highlight ruby %}
# PS Code from NestJS page
# Main module. Make it global.
{
   provide: APP_GUARD,
   useClass: JwtAuthGuard,
 },

# Decorator and constant
export const IS_PUBLIC_KEY = 'isPublic';
export const Public = () => SetMetadata(IS_PUBLIC_KEY, true);

# Improve the guard
@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {
  constructor(private reflector: Reflector) {
    super();
  }

  canActivate(context: ExecutionContext) {
    const isPublic = this.reflector.getAllAndOverride<boolean>(IS_PUBLIC_KEY, [
      context.getHandler(),
      context.getClass(),
    ]);
    if (isPublic) {
      return true;
    }
    return super.canActivate(context);
  }
}

# Add the decorator where should skip the authentication
@Public()
@Get()
findAll() {
  return [];
}

{% endhighlight %}


<br />
<h3><u id="authorization">Authorization</u></h3>

<p style="text-align: justify;"><em><a href="https://docs.nestjs.com/security/authorization">Authorization</a> refers to the process that determines what a user is able to do.</em></p>

<p>The authorization is regarding define roles to filter what can be access or not. The complete example you can see in the <a href="https://docs.nestjs.com/security/authorization">NestJS page</a>.</p>


<br />
<h3><u id="encryptation">Encryption and Hashing</u></h3>

<p style="text-align: justify;"><em>Encryption is the process of encoding information. Hashing is the process of converting a given key into another value. <a href="https://docs.nestjs.com/security/encryption-and-hashing">[1]</a></em></p>

<p style="text-align: justify;">One example is <a href="https://github.com/fabiana2611/nestjs2/blob/master/messages-level-3/src/auth/auth.controller.ts">signup a new user</a>. The codes to create the new password are below.</p>

<p style="text-align: justify;">Here is the first example using a random series of numbers and letters, salt, to improve the security. After generate that number, the password and salt are concatenate to create the hash number. The last step is concatenate the result and the original salt value. It will make available to validate the password.</p>

{% highlight ruby %}
# auth.util.ts
public async buildPassword(password: string) {
   // hash the user pws
   //Generate Salt
   const salt = randomBytes(8).toString('hex');

   //Hash the salt and pwd
   const hash = (await scrypt(password, salt, 32)) as Buffer;

   // Join the hashed result and salt
   const result = salt + '.' + hash.toString('hex');

   return result;
 }

# Request
POST localhost:3001/auth/v1/signup
{
 "email": "myemail@example.com",
 "password": "123"
}

# Response
{
 "id": 1,
 "email": "myemail@example.com",
 "password": "84c8d22ec8631fd0.669f933ae6f058c053831fa4770687f813f1b973e1b86c3067a74605894d0d71"
}
{% endhighlight %}

<p>A second version is using exactly what nestjs documentation show.</p>

{% highlight ruby %}
# auth.util.js
public async buildPasswordV2(password: string) {
  const iv = randomBytes(16);
  const word = 'Word used to generate key';
  const key = (await promisify(scrypt)(word, 'salt', 32)) as Buffer;
  const cipher = createCipheriv('aes-256-ctr', key, iv);

  const encryptedText = Buffer.concat([
    cipher.update(password),
    cipher.final(),
  ]);

  return encryptedText.toString();
}

# Request
POST localhost:3001/auth/v2/signup
{
 "email": "myemail@example.com",
 "password": "123kjhkjhyutu"
}

# Response
{
  "id": 1,
  "email": "myemail@example.com",
  "password": "\r@o\u0013�g�%g���"
}
{% endhighlight %}

<p>A third version is using what nestjs documentation show with hash using the library bcrypt.</p>

{% highlight ruby %}
public async buildPasswordV3(password: string) {
  const salt = await bcrypt.genSalt();
  return await bcrypt.hash(password, salt);
}

public async isPwdValidV3(password: string, userPassword: string) {
  return await bcrypt.compare(password, userPassword);
}
{% endhighlight %}



<br />
<h3><u id="helmet">Helmet</u></h3>

<p><em><a href="https://docs.nestjs.com/security/helmet">Helmet</a> can help protect your app from some well-known web vulnerabilities by setting HTTP headers appropriately. </em></p>

{% highlight ruby %}
# Install
$ npm i --save helmet

# main.ts
 app.use(helmet);

{% endhighlight %}


<br />
<h3><u id="cors">CORS</u></h3>

<p style="text-align: justify;"><em><a href="https://docs.nestjs.com/security/cors">Cross-origin resource sharing</a> (CORS) is a mechanism that allows resources to be requested from another domain. Under the hood, Nest makes use of the Express cors package.</em></p>

{% highlight ruby %}
# main.ts
app.enableCors();
{% endhighlight %}

<br />
<h3><u id="csrf">CSRF Protection</u></h3>

<p style="text-align: justify;"><a href="https://fabiana2611.github.io/java/vulnerability#csrf">Cross-Site Request Forgery</a>: unauthorized command from a trusted user. A good way to prevent this kind of attack is using tokens. <p.>

<p>Nestjs has the <a href="https://docs.nestjs.com/security/csrf">package csurf</a> to mitigate this risk. It needs session middleware or cookie-parser.</p>

{% highlight ruby %}
# install
$ npm i --save csurf

# main.js
import * as csurf from 'csurf';

app.use(csurf());
{% endhighlight %}


<br />
<h3><u id="ratelimiting">Rate limiting</u></h3>

<p style="text-align: justify;"><em>The <a href="https://docs.nestjs.com/security/rate-limiting">rate-limiting</a>is a common technique to protect applications from brute-force attacks.</em></p>

<p style="text-align: justify">In the example, regarding the ThrottlerModule, the 'ttl' attribute is the time to live and the 'limit' is the quantity of request to the 'ttl'. Also, you see the guard used to handle that. Here it is global, but not mandatory. There is possibility, for example, to customize it or use decorators.</p>

{% highlight ruby %}
# install
$ npm i --save @nestjs/throttler

# MessageModule
@Module({
  imports: [
    AuthModule,
    ConfigModule.register({ attribute: 'staging' }),
    ThrottlerModule.forRoot({
      //time to live
      ttl: 60,
      limit: 10,
    }),
  ],
  providers: [
  MessagesService,
  MessagesRepository,
  { provide: APP_GUARD, useClass: ThrottlerGuard },
],
  controllers: [MessagesController],
})
export class MessagesModule {
{% endhighlight %}
