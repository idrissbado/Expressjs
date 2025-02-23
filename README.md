# Car Driver Lab - Web Application

## Overview
This project is a web application built using **Express.js** that includes three main pages:

- **Home Page**
- **Our Services**
- **Contact Us**

The application is designed to be accessible **only during working hours** (Monday to Friday, from 9 AM to 5 PM). If a user tries to access the site outside these hours, they will receive a message indicating that the service is unavailable.

## Features
- A navigation bar with links to all pages.
- A custom middleware function to check working hours before serving the pages.
- Styled using CSS for better UI experience.
- Uses a template engine (EJS) to render dynamic content.

## Installation & Setup

### Prerequisites
Make sure you have **Node.js** and **npm** installed on your system.

### Steps to Run the Project
1. Clone this repository:
   ```sh
   git clone <repository-url>
   cd car-driver-lab
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the server:
   ```sh
   node index.js
   ```
4. Open your browser and go to:
   ```
   http://localhost:3000
   ```

## Project Structure
```
car-driver-lab/
│── public/            # CSS and static files
│── views/             # EJS templates
│   ├── home.ejs       # Home page
│   ├── services.ejs   # Our Services page
│   ├── contact.ejs    # Contact Us page
│── index.js           # Main server file
│── middleware.js      # Custom middleware for time checking
│── package.json       # Dependencies and scripts
```

## Middleware for Time Restriction
A custom middleware is used to **restrict access** outside working hours. This function checks the current time and only allows access between **Monday-Friday (9 AM - 5 PM).**

### **middleware.js**
```javascript
function workingHoursMiddleware(req, res, next) {
    const now = new Date();
    const day = now.getDay(); // 0 (Sunday) to 6 (Saturday)
    const hour = now.getHours(); // 0 to 23

    if (day >= 1 && day <= 5 && hour >= 9 && hour < 17) {
        next(); // Proceed to the requested route
    } else {
        res.send("Sorry, we are only available Monday to Friday from 9 AM to 5 PM.");
    }
}

module.exports = workingHoursMiddleware;
```

## Express Server Setup
The server is set up with routes for the three pages, and the **middleware** is applied globally to restrict access based on time.

### **index.js**
```javascript
const express = require("express");
const app = express();
const workingHoursMiddleware = require("./middleware");

app.set("view engine", "ejs");
app.use(express.static("public"));
app.use(workingHoursMiddleware);

app.get("/", (req, res) => {
    res.render("home");
});

app.get("/services", (req, res) => {
    res.render("services");
});

app.get("/contact", (req, res) => {
    res.render("contact");
});

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

## Conclusion
This project demonstrates how to build a simple **Express.js web application** with middleware functionality for **time-based access control**. The application is styled using CSS and dynamically rendered using **EJS templates**.

Feel free to enhance the project by adding more features such as a database, authentication, or an API!

---

### Author
Developed by **Idriss BADO**
