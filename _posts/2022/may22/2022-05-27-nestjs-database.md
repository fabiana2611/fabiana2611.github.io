---
layout: post
title:  "NestJS - Database"
date:   2022-05-27
categories: node
permalink: /:categories/nestjs-database
---

<p style="text-align: justify;">This post has some notes and the code I did while studying nestjs. The idea is to code and see the database configured and ready to start some applications to use the database. </p>

<p style="text-align: justify;">Nest can work with different database, SQL or NoSQL. You just need use the correct driver. The general libraries to Node.JS are MikroORM, Sequelize, TypeORM (most mature for TypeScript) and Prisma. The NodeJS provides tight integration with @nestjs/typeorm, @nestjs/sequelize and @nestjs/mongoose. You can use more than one instance of the database and different combinations of the database libraries.</p>

<p>Here are examples how to configure the main supports to database. The database config you can add in the AppModule or in a separate file. The code you can see <a href="https://github.com/fabiana2611/nestjs2">here</a>.</p>


<h3>TypeORM</h3>

<p>More details about the use of configurations with configService or external files and about the sort of relations between the entities you can see here<a href="https://docs.nestjs.com/techniques/database">[1]</a>, <a href="https://docs.nestjs.com/recipes/sql-typeorm">[2]</a>, <a href="https://docs.nestjs.com/techniques/database#relations">[3]</a>.</p>

{% highlight ruby %}
$ npm install --save @nestjs/typeorm typeorm pg

# AppModule
@Module({
  imports: [
    UsersModule,
    UserHttpModule,
    TypeOrmModule.forRoot({
      type: 'postgres',
      port: 5432,
      username: 'postgres',
      password: '',
      database: 'postgres',
      synchronize: true,
      host: 'localhost',
      entities: [User],
    }),
    TypeOrmModule.forRoot({
      type: 'postgres',
      port: 5433,
      username: 'postgres',
      password: '',
      database: 'postgres',
      synchronize: true,
      name: 'OldConnection',
      host: 'localhost',
      entities: [UserOld],
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
{% endhighlight %}

<h3>Sequelize</h3>

<p>More details about the use of configurations with configService or external files an the relations between the entities you can see here<a href="https://docs.nestjs.com/techniques/database">[1]</a>, <a href="https://docs.nestjs.com/recipes/sql-sequelize">[4]</a>, <a href="https://docs.nestjs.com/techniques/database#relations-1">[5]</a>.</p>

{% highlight ruby %}
$ npm install --save @nestjs/sequelize sequelize sequelize-typescript pg
$ npm install --save-dev @types/sequelize


# AppModule
@Module({
  imports: [
    UsersModule,
    SequelizeModule.forRoot({
      dialect: 'postgres',
      host: 'localhost',
      port: 5432,
      username: 'postgres',
      password: '',
      database: 'postgres',
      synchronize: true,
      models: [UserModel],
    }),
    SequelizeModule.forRoot({
      dialect: 'postgres',
      host: 'localhost',
      port: 5433,
      username: 'postgres',
      password: '',
      database: 'postgres',
      models: [UserOldModel],
      synchronize: true,
      name: 'OldConnection',
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}

# Who use
@Module({
  imports: [
    SequelizeModule.forFeature([UserModel]),
    SequelizeModule.forFeature([UserOldModel], 'OldConnection'),
  ],
  providers: [UsersService],
  exports: [SequelizeModule],
  controllers: [UsersController],
})
export class UsersModule {}

{% endhighlight %}

<h3>Prisma</h3>

<p>More details you can find <a href="https://docs.nestjs.com/recipes/prisma">here</a>.</p>

{% highlight ruby %}
$ npm install -g @nestjs/cli
$ nest new hello-prisma
$ cd hello-prisma
$ npm install prisma --save-dev
$ npx prisma
$ npx prisma init
{% endhighlight %}

<p>After those steps your project will be created with a folder prisma and the schema file where you will add your entities. In this case you don't need declare the configuration in the module. You will do this in your .env file. For all the other libraries is possible use the .env file to that as well but prisma has it as default.</p>

<p>Here is the example how it works. The complete code you can see <a href="https://github.com/fabiana2611/nestjs2/tree/master/database-prisma">here</a>.</p>

{% highlight ruby %}
# prism/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

model User {
  id    Int     @default(autoincrement()) @id
  email String  @unique
  name  String?
  posts Post[]
}

# Service using prisma
constructor(private prisma: PrismaService) {}

async user(
  userWhereUniqueInput: Prisma.UserWhereUniqueInput,
): Promise<User | null> {
  return this.prisma.user.findUnique({
    where: userWhereUniqueInput,
  });
}
{% endhighlight %}
