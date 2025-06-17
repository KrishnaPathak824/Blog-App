# Backend - Postgres and environments setup

---

## 1. Install Postgres in windows

[Installation](https://www.postgresql.org/download/windows/)

![alt](/materials/Task2/Step1.png)

---

## 2. Setup postgres and create database in postgres according to the env.

![alt](/materials/Task2/Step2.png)

- Create a new user
  `CREATE USER fellowship WITH PASSWORD 'hello123';`
- Create a new database
  `CREATE DATABASE fellowship;`

- Give full access on the new DB to the user
  `GRANT ALL PRIVILEGES ON DATABASE fellowship TO fellowship;`

`permission denied for schema public` error had arised.
This error meant that the user fellowship does not have permission to create tables in the public schema of your PostgreSQL database.

So the privileges are given to the fellowship user.
`GRANT ALL PRIVILEGES ON SCHEMA public TO fellowship;`
`ALTER SCHEMA public OWNER TO fellowship;`

Navigate to create database,user and password from the env file.

![alt](/materials/Task2/Step3.png)

---

## 3. Create a clerk application.

Vist [Clerk](https://clerk.com/docs/quickstarts/react)

Setup the Clerk punishable key in your frontend

`VITE_CLERK_PUBLISHABLE_KEY=pk_test_cmVndWxhci1zYXR5ci0zMS5jbGVyay5hY2NvdW50cy5kZXYk`

Setup the Clerk punishable key and secret key in the backend.

`CLERK_PUBLISHABLE_KEY=pk_test_cmVndWxhci1zYXR5ci0zMS5jbGVyay5hY2NvdW50cy5kZXYk`
`CLERK_SECRET_KEY=sk_test_tFTEZn6QogIWeBc8XBLVt4juxAIEXzz2Coyg9Dc6Mv`

Now, google login feature is implemented in the application.

![alt](/materials/Task2/Step5.png)

---

## 4. Run migrations in the both backend repositories.

`npm run migrate` runs migration in both the backend.

All the tables in the database is listed.
![alt](/materials/Task2/Step4.png)

---

## 5. Application should run smoothly.

User can view all the blogs.
![alt](/materials/Task2/Step7.png)

User can create a blog.
![alt](/materials/Task2/Step6.png)

User can view a certain blog.

![alt](/materials/Task2/Step8.png)

User can view all the comments in the post and create a comment.

![alt](/materials/Task2/Step9.png)

---

## 6. Use winston package to create a logger file for each request and error.

- Add winston package to the project `yarn add winston`

- Creates a logger that captures and formats logs.

- Logs are saved to files based on their severity level info and error.

- The log formats are defined where it adds a timestamp, includes error stack and outputs everything as json.

- The transports logs/request.log and saves the level info in it.

- The transports logs/error.log and saves the level error in it.

![alt](/materials/Task2/Step10.png)

Middleware which runs on every incoming requesr and logs useful request data like method, URL, and body.It sends the log to your logger, which saves it to request.log.

![alt](/materials/Task2/Step11.png)

The errorHandler middleware contains the logger for error which logs the error with error message,stack trace HTTP method and route

![alt](/materials/Task2/Step12.png)

The middleware requestLogger works for all incoming requests and the error logger runs in the errorHandler middleware if any error is catched.

![alt](/materials/Task2/Step13.png)

The log files create these kinds of logs.

![alt](/materials/Task2/Step15.png)

![alt](/materials/Task2/Step14.png)

---
