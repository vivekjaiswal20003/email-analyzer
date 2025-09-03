# Email Header Analyzer: 

## Project Overview
 Just paste a raw email header, and it will dissect it to reveal the email's path, authentication checks, and even identify the service provider that handled it. 

## Key Features
*   **Header Deep Dive:** Extracts and interprets all the details hidden within email headers.
*   **Authentication Insights:** Get the lowdown on SPF, DKIM, and DMARC statuses – crucial for verifying an email's legitimacy.
*   **ESP Spotter:** Automatically identifies the Email Service Provider (like Gmail, Outlook, or even LinkedIn) that played a role in the email's delivery.
*   **History at Your Fingertips:** All analyzed headers and their processed data are saved to a MongoDB database, so you can revisit them anytime.
*   **Sleek & Responsive UI:** A clean, intuitive, and mobile-friendly interface crafted with React and Material-UI, making analysis a breeze on any device.
*   **Robust NestJS Backend:** Built on a solid NestJS foundation, ensuring a well-structured, scalable, and maintainable API with best practices baked in (DTOs, validation, config, error handling).

## Tech Stack

### Frontend
*   **React:** For building the interactive user interface.
*   **Material-UI (MUI):** My go-to UI library for beautiful, responsive components.
*   **Axios:** For making those essential HTTP requests to the backend.

### Backend
*   **NestJS:** A Node.js framework that brings structure and scalability to server-side development.
*   **TypeScript:** Keeps the codebase robust and maintainable with strong typing.
*   **Mongoose:** My ORM of choice for interacting with MongoDB.
*   **Mailparser:** parse those complex email headers.
*   **Class-validator & Class-transformer:** For ensuring incoming data is always valid and well-formed.
*   **@nestjs/config:** For managing environment variables .

### Database
*   **MongoDB:** A flexible NoSQL database for storing all the email analysis data.

## Project Structure

```
E:\email-imap\
├───backend\
│   ├───src\
│   │   ├───common\
│   │   │   └───filters\
│   │   │       └───http-exception.filter.ts
│   │   ├───config\
│   │   │   ├───configuration.ts
│   │   │   └───config.module.ts
│   │   ├───email\
│   │   │   ├───dto\
│   │   │   │   └───analyze-header.dto.ts
│   │   │   ├───schemas\
│   │   │   │   └───email.schema.ts
│   │   │   ├───utils\
│   │   │   │   └───esp-detector.ts
│   │   │   ├───email.controller.ts
│   │   │   ├───email.module.ts
│   │   │   └───email.service.ts
│   │   ├───app.module.ts
│   │   └───main.ts
│   ├───package.json
│   └───... (node_modules, etc.)
└───frontend\
    ├───src\
    │   ├───components\
│   │   │   ├───AnalysisDisplay.js
│   │   │   └───HopTimeline.js
│   │   ├───App.js
│   │   ├───index.css
│   │   └───index.js
│   ├───package.json
│   └───... (node_modules, public, etc.)
```

## Getting Started

### Prerequisites
Before you begin, make sure you have:
*   Node.js (v18 or newer is recommended)
*   npm (Node Package Manager)
*   A running MongoDB instance (either locally or a cloud service like MongoDB Atlas)

### 1. Setting Up the Backend
First, let's get the server running:
```bash
cd backend
npm install # Install all the necessary backend dependencies
```
Next, you'll need to tell the backend how to connect to your MongoDB. Create a `.env` file in the `backend` directory and add your connection string:
```
MONGO_URI="your_mongodb_connection_string_here"
```
(e.g., `MONGO_URI="mongodb+srv://user:password@cluster0.xxxx.mongodb.net/email-analyzer?retryWrites=true&w=majority"`)

Now, fire up the backend server:
```bash
npm run start
```
You should see the backend running, typically on `http://localhost:5000`.

### 2. Setting Up the Frontend
In a *new* terminal window, let's get the UI ready:
```bash
cd frontend
npm install # Grab all the frontend dependencies
```
Then, launch the frontend development server:
```bash
npm start
```
Your browser should automatically open to `http://localhost:3000`, where you'll see the application.

## How to Use It
1.  Make sure both your backend and frontend servers are up and running.
2.  Head over to `http://localhost:3000` in your web browser.
3.  Paste a raw email header (you can usually find this by viewing the "original" or "raw" message in your email client) into the large text area.
4.  Hit that "Analyze" button!
5.  The app will display a detailed breakdown of the email, including who sent it, who received it, the subject, all the authentication checks (SPF, DKIM, DMARC), the detected email service provider, and a cool visual timeline of its journey.

## Backend API Endpoint

### `POST /api/emails/analyze`
This is where the magic happens! Send your raw email headers here for analysis and storage.
*   **Request Body:**
    ```json
    {
      "header": "Your raw email header string goes here..."
    }
    ```
*   **Response:** You'll get back the fully parsed email object, complete with `espType` and `authenticationResults`.

## What's Next? (Future Ideas & Roadmap)

future scopes for this project:

*   **Deeper Email Analysis:**
    *   **Spam/Phishing Flags:** Implement smarter checks to flag potentially malicious emails based on header anomalies or known spam patterns.
    *   **Security Audit:** Automatically highlight specific security vulnerabilities found in the headers.
*   **Enhanced User Experience:**
    *   **Analysis History Dashboard:** A dedicated page where users can browse, search, and re-view all their past analyzed emails.
    *   **Interactive Elements:** Make IP addresses clickable for instant WHOIS lookups, or domains clickable for DNS details.
    *   **Dark Mode!** Because who doesn't love a good dark theme?
*   **Backend & Infrastructure Polish:**
    *   **Rate Limiting:** Protect the API from excessive requests.
    *   **Smart Caching:** Cache analysis results for frequently submitted headers to speed things up.
    *   **Asynchronous Processing:** For those really massive headers, process them in the background to keep the UI snappy.
    *   **API Documentation (Swagger):** Integrate `@nestjs/swagger` for beautiful, auto-generated, interactive API docs.
*   **Development & Deployment:**
    *   **Comprehensive Testing:** Beef up the test suite with more unit, integration, and end-to-end tests.
    *   **CI/CD Pipeline:** Set up automated workflows for testing and deployment 

---