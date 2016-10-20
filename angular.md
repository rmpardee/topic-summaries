## Terminology

* View: HTML with additional functionality

* Controller: where your functionality is
- in the router (.config after creating the app) is where you attach a specific view to a specific controller
- involves using `$scope`
- Add to HTML with `<div ng-controller="[name of controller]">`

* Factory: Sharing data between Controllers
- Basically a bunch of functions that you can reuse throughout other controllers (a toolbelt)
- Returns a single object of functions that can be injected into other controllers

* Service: Same as a Factory, but instantiated with the `new` keyword.

* Directives: can be:
- a new HTML element you define
- an attribution on an element
- the class of an element
- You can create custom ones, or use build-in ones (like `ng-repeat`)


## In index.html

1. You have to add your app itself with `ng-app`:

`<html ng-app='[app name here]'>`

2. If you're using ngRoute (which you likely are), you'll need `ng-view`. This is what will actually show all the views you make.

`<div ng-view></div>`

## In app.js (sometimes called index.js)

1. Here is where you actually define your app. Make a new module called whatever you named your app in index.html:

```js
angular.module('[app name here]', [
  
  [Here is where you'll add all the things you want to extend your app with. This will likely be your services, authentication, and almost always ngRoute. Anything you want your app to be able to use, you need to list here
    '[app name here].services',
    '[app name here].auth',
    'ngRoute',
    etc...
  ]

])
```

2. Set your routes with ngRoute. You are chaining this `.config` directly onto the module you made above (your app), and telling it which views should be shown when the URL on the client points to a specific route.



```js
.config(function ($routeProvider, $httpProvider) {
  $routeProvider

    [can be whatever, here are some examples:

    .when('/signin', {
      templateUrl: 'app/auth/signin.html',
      controller: 'AuthController'
    })
    .when('/signup', {
      templateUrl: 'app/auth/signup.html',
      controller: 'AuthController'
    })
    
    ... etc ... And you'll likely also want:

    .otherwise({
      redirectTo: '/home'

    ]

  [might use $httpProvider here as well]

});
```

## Make your controllers

Make separate files for each of the controllers your using in your .config in app.js.
* The angular module should be named the same thing you listed in the array when creating your app
* The name of the controller should be named the same thing you use when you set up your routes in app.js

Will generally look like:

```js
angular.module('[your app name].[whatever you called it when defining your app]', [])

.controller('[whatever name you used in your router]', function ($scope, [whatever factories you need]) {

  [Here you'll likely be adding things to $scope, and using the functions from your factory you passed in (your toolbelt)]

});
```

