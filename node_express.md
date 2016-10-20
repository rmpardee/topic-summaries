## In your server.js file

1. Create the app itself as an invocation of express.

`var app = express();`

2. Invoke your middlewares and routes by requiring those files, and passing in your app and express itself.

> Note that you can't just require the app in the middleware or routes file. You need to actual create the routes and apply middleware in the same file you create the app, so by wrapping your middleware and routes in functions and then requiring and invoking those functions in the server.js file, you are getting around that while keeping things modular.

```js
require('./config/middleware.js')(app, express);
require('./config/routes.js')(app, express);
```

3. Listen to your port.

a. Create your port variable that defaults to the environment if established (if deployed), or a hard-coded number if running locally

`var port = process.env.PORT || 3000;`

b. Have your app listen on this port

`app.listen(port);

4. Export your app

`module.exports = app;`


## In your middleware.js file

1. Wrap the entiredy of your middleware in an anonymous function that takes in an app and express itself (this is what you are requiring in server.js so it can be invoked there).

```js
module.exports = function (app, express) {

  [... middleware goes here]

};
```

2. Add the middleware you want with `app.use()`.
Almost always you will want body-parser (require it at the top of the file!) and to actually serve your client (These all go inside your anonymous fn from #1).

```js
app.use(bodyParser.urlencoded({extended: true}));
app.use(bodyParser.json());
app.use(express.static(__dirname + '/../../client'));
```

3. If you have any custom middleware you can either define it here, or have it in another file and require it at the top and pass it in to `app.use()`.

## In your routes.js file

1. Same as with middleware, wrap the entiredy of your routes in an anonymous function that takes in an app and express itself (this is what you are requiring in server.js so it can be invoked there).

```js
module.exports = function (app, express) {

  [... routes go here]

};
```

2. Add the routes you want with `app.get()` and `app.post()`. The first parameter in these will be a string showing the API route they work for, and the second is what function should be invoked when that route is called, which takes in a request, and response, and optional next function to be called when it's finished (These all go inside your anonymous fn from #1).

```js
app.get('/api/users/login', function(req, res) {

  [What happens goes here. Often its:
    1. Communicating with the database.
    * You'll need your model and/or ORM
    * You'll often use req.body.[something]

    2. Often some kind of promise
    * You'll need a promise library

    3. Sending back some response
    * You'll often use res.send([code here, like 200]) or res.json({ [etc...] }) to explicitly send back data
  ]

});
app.post('/api/users/signup', function(req, res) {
  
  [What happens goes here, see above ^.]

});
```

> Note: often the function you're passing into app.get() or app.post() as the second parameter are defined in a controller (a separate file). Each function there will still need to take in a request and response just as they would if passed as an anonymous function. Make sure to require your ORM and promise library in whatever file you're actually writing these functions.

> You might also see express.Router() used. This can be a nice way to separate different types of routers that you want (for example one for users, and a separate one for whatever other API calls your app will be making).