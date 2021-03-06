## DOCUMENTATION

## DEVELOPMENT

### Docker
- Built on lightweight docker image "node:8-alpine" (see Dockerfile)
- Command lines to launch docker images:
  - `yarn docker:dev` launch project in DEV mode
  - more... (see package.json)

### Platforms
- Mainly tested on MacOS High Sierra, node 8.10.x, yarn
- Also tested on Windows 10 (Powershell) with MongoDB, latest nodejs, yarn

### Other Tools
- Use Postman to try out APIs
  - By default, APIs run on HTTPS localhost, so turn off "SSL Certificate Verification" in Postman Settings.

## FEATURES

### Add a new API Route:
- Steps to create a new route:
  - src/api/routes/your-new-route.route.ts
  - src/api/controllers/route-controller.ts
  - src/api/routes/v1/index.ts - add your route
- Example: [../src/api/routes/v1/user.route.ts](../src/api/routes/v1/user.route.ts) (CRUD routes for user endpoints)

### API Controller
- An API Route is assigned with an API Controller to handle that route
- Example of user controller that runs user.model's functions:
  - [../src/api/controllers/user.controller.ts](../src/api/controllers/user.controller.ts)
  - [../src/api/models/user.model.ts](../src/api/models/user.model.ts) (see "transform" and "list" functions)

### API - Upload File /upload/file
- Using "multer" to parse form (file) data & store files to "/uploads"
- Example: POST https://localhost:3009/v1/upload/file
  - set Authorization: Bearer TOKEN, Content-Type: application/x-www-form-urlencoded
  - set form-data, field "file" and select a file to upload
  - uploaded file will be stored in "/uploads" directory
- Example: [../src/api/routes/v1/upload.route.ts](../src/api/routes/v1/upload.route.ts)

### API - Forgot Password /forgot-password
- a POST handler to generate a one-time temporary password, then email it to an existing user.
- Example: [../src/api/controllers/auth.controller.ts](../src/api/controllers/auth.controller.ts)

### Slack
- Obtain your Slack Incoming Webhook (tie to a channel) from your Slack account & put it in .env file
- Example: [../src/api/controllers/auth.controller.ts](../src/api/controllers/auth.controller.ts) (send slack a message after user registered (POST v1/auth/register))

### Send Email
- Using "nodemailer" to send email
- Using "handlebars" to get email templates: welcomeEmail({ name: 'John Doe', email: 'emailexample@gmail.com' })
- Obtain your Mailgun API Key & Email Domain (use sandbox domain name for testing) & put it in .env file
- Example: [../src/api/controllers/auth.controller.ts](../src/api/controllers/auth.controller.ts) (send email after user registered (POST v1/auth/register))
