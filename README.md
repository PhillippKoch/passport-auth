# Passport Authentication for node server

Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based web application. A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.


## Getting Started

Start by either downloading the zip file or clone with HTTPS.

### Prerequisites

* Node 
* NPM
* Command-Line
* Code editor like Atom, VS Code
* A web browser like Safari, Google Chrome

## Running

#### Disclaimer - Change the database configurations in your server file explained below according to your preferences, but you may as well leave them and move on, if you're using MongoDB already.

### 1. Install all dependencies
From your terminal, install all dependencies for the application.
```
npm install
```

### 2. Connect your database
* Require mongoose package (elegant mongodb object modeling for node.js)
```
const mongoose = require("mongoose")
```
* Connect to a local database
```
mongoose.connect("mongodb://localhost/auth", {useNewUrlParser: true});
```

### 3. Passport configurations
* Require the following passport packages
```
const passport = require("passport")
csont LocalStrategy = require("passport-local")
const passportLocalMongoose = require("passport-local-mongoose")
```
* Further configurations for express-session (cookie based session middleware) and passport to serialize and deserialize user
```
// requiring express-session and passing an object used during authenication
app.use(require("express-session")({
    secret: "be as silly as you can be while initializing this secret string",
    resave: false,
    saveUninitialized: false
}));
// telling express to use passport.initialize() and passport.session()
app.use(passport.initialize());
app.use(passport.session());
// telling passport to use local strategy for authentication
passport.use(new LocalStrategy(User.authenticate()));
// serialize and deserialize user on authenication
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());
```

### 4. Middleware configurations
Middleware function to check is user is still logged in or not

```
function isLoggedIn(req, res, next){
    if(req.isAuthenticated()){
        return next();
    }
    res.redirect("/login");
}
```

### 5. Logout route
```
app.get('/logout', function (req, res){
  req.session.destroy(function (err) {
    res.redirect('/'); //Inside a callback… bulletproof!
  });
});
```

## Built With

* [Node.js] (https://nodejs.org/en/) - Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.
* [Express] (https://expressjs.com/) - Fast, unopinionated, minimalist web framework for Node.js
* [Passport] (http://www.passportjs.org/) - Simple, unobtrusive authentication for Node.js
* [Passport-Local] (http://www.passportjs.org/packages/passport-local/) - Passport strategy for authenticating with a username and password.
* [Passport-Local-Mongoose] (https://github.com/saintedlama/passport-local-mongoose) - Passport-Local Mongoose is a Mongoose plugin that simplifies building username and password login with Passport
* [Express-Session] (https://expressjs.com/en/resources/middleware/cookie-session.html) - Simple cookie-based session middleware.
* [Javascript] (https://www.javascript.com/) - High-level, interpreted programming language
* [HTML] (https://www.html.com/) - Standard markup language

## Authors

* **Vasu Goel** (https://github.com/VasuGoel)

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/VasuGoel/passport-auth/blob/master/LICENSE) file for details

## Acknowledgments

* Adding authentication on a college project website

