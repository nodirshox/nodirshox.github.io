---
layout: post
title: "Solve Prisma “ERROR: column “x” of relation “y” contains null values”"
categories: ["tutorial", "programming", "nodejs"]
permalink: /solve-prisma-error-column-x-of-relation-y-contains-null-values
---

Have you faced such an error while applying migrations to the production database?

```
Database error:
ERROR: column "x" of relation "y" contains null values
```

or this warning message in the migration SQL file?

```
Added the required column x to the y table without a default value. This is not possible if the table is not empty.
```

Let’s dive into the situation and problem.

To start with I am going to reproduce this error. Initial [source code](https://github.com/nodirshox/nestjs-prisma-starter){:target="_blank"}.

1-I have 2 models:

```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  createdAt DateTime @default(now()) @map(name: "created_at")

  @@map(name: "users")
}

model Task {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  createdAt   DateTime @default(now()) @map(name: "created_at")

  @@map(name: "tasks")
}
```

2-Generate initial migration

```
npx prisma migrate dev --name init
```

3-Apply migration in the production database (change production database URL in .env file)

```
npx prisma migrate deploy
```

4-Add data in production users and tasks table from API endpoint. I used Postman tool.

![Screenshot](/assets/2023-04-23-prisma-error/prisma-1.jpg)

![Screenshot](/assets/2023-04-23-prisma-error/prisma-2.jpg)

5-Our application business logic is changed, and I want to make changes in Prisma file. Added Tasks reference in User model and required user reference in Task model.

```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  createdAt DateTime @default(now()) @map(name: "created_at")

  Tasks Task[]

  @@map(name: "users")
}

model Task {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  createdAt   DateTime @default(now()) @map(name: "created_at")

  userId Int  @map("user_id")
  User   User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map(name: "tasks")
}
```

6-Let’s create a migration for this change:

```
npx prisma migrate dev --name task
```

![Screenshot](/assets/2023-04-23-prisma-error/prisma-3.jpg)

It ran successfully. Because there is no data in my local database.

Let’s look at the migration file:

```
/*
  Warnings:

  - Added the required column `user_id` to the `tasks` table without a default value. This is not possible if the table is not empty.

*/
-- AlterTable
ALTER TABLE "tasks" ADD COLUMN     "user_id" INTEGER NOT NULL;

-- AddForeignKey
ALTER TABLE "tasks" ADD CONSTRAINT "tasks_user_id_fkey" FOREIGN KEY ("user_id") REFERENCES "users"("id") ON DELETE CASCADE ON UPDATE CASCADE;
```

It includes a warning message.

7-Let’s try to apply this migration to the production database with data (tasks table).

![Screenshot](/assets/2023-04-23-prisma-error/prisma-4.jpg)

Oh noooooo. We have a huge problem.

The problem is we want to add the required ‘user_id’ in tasks table. That’s why Prisma migration stopped.

# Solution steps [(Reference)](https://stackoverflow.com/a/67868930/10702502){:target="_blank"}

1. Create the fields first as optional and then run migrate
2. Fill the fields first with the required data.
3. Remove the optional (?) from the field.

---

1-Let’s go back 5-step, and make the correct migration change for the initial step.

```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  createdAt DateTime @default(now()) @map(name: "created_at")

  Tasks Task[]

  @@map(name: "users")
}

model Task {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  createdAt   DateTime @default(now()) @map(name: "created_at")

  userId Int?  @map("user_id")
  User   User? @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map(name: "tasks")
}
```

2-Create migration

```
npx prisma migrate dev --name optional-user
```

3-Apply latest migration to production database

```
npx prisma migrate deploy
```

Now, it user_id column is added

![Screenshot](/assets/2023-04-23-prisma-error/prisma-5.jpg)

4-Fill rows with some default value. You can write script to fill the values.

![Screenshot](/assets/2023-04-23-prisma-error/prisma-6.jpg)

5-Let’s remove the optional field in Prisma

```
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String
  createdAt DateTime @default(now()) @map(name: "created_at")

  Tasks Task[]

  @@map(name: "users")
}

model Task {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  createdAt   DateTime @default(now()) @map(name: "created_at")

  userId Int  @map("user_id")
  User   User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map(name: "tasks")
}
```

6-Create migration

```
npx prisma migrate dev --name remove-optional-user
```

7-Apply latest migration to production database

```
npx prisma migrate deploy
```

![Screenshot](/assets/2023-04-23-prisma-error/prisma-7.jpg)

Finally, we solved the error.

[Link](https://medium.com/@nodirshox-e/solve-prisma-error-column-x-of-relation-y-contains-null-values-6079a5721b1d){:target="_blank"}
