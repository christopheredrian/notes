
Introduction
===============

Why Angular?
- For building dynamic websites
    - Organizes javascript code
    - Fast website creation
    - Plays well with jquery
    - Easy to test
**Modern API-Drive Application**
One api for
    - Browser
    - Mobile
    - Developers

Requirements
---------------
1. angular.min.js
2. Optional - bootstrap

Directives
-------------
_A marker(attr) on a HTML tag that tells Angular to run some JavaScript code_

```html
<!DOCTYPE html>
<html>
<body ng-controller="MyController">

</body>
</html>



```

Modules - keeping our code encapsulated
------------------------------------------------
- Where we write pieces of our Angular application
- Makes our code more maintainable, testable and readable
- Where we define dependencies for our app

###Module Creation

```javascript
var app = angular.module('app name', [] - dependencies);
```

Expressions
------------
- Allows you to insert dynamic values into HTML

```html
<p>
    5 plus 10 is {{ 5 + 10}}
</p>


```

Skeleton(Hello World)
----------------

```html

<!DOCTYPE html>
<!-- This will Run the module name on the app.js file -->
<html ng-app="store">
<head>
    <title></title>
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css">
</head>

<body>
<p>Hello {{"world!"}}</p>
<script type="text/javascript" src="angular.min.js"></script>
<script type="text/javascript" src="app.js"></script>

</body>
</html>

```

On javascript

```javascript
var app = angular.module('app name', [] - dependencies);
```


Controllers
--------------
- Where we define our apps' behavior by defining functions and values
####How
1. Create the controller
2. Set values to the controller

```javascript

(function(){
    var app = angular.module('store', []);
    var guitar = {
        name: 'Stratocaster',
        brand: 'Fender',
        price: 549,
        description: 'Used by Jimi Hendrix',
        canPurchase: false
    };
    // Controller name : camel case, postfixed : 'Controller'
    app.controller('StoreController', function(){
        // Set properties for the controller
        this.product = guitar;
    });

})();
```

3. On HTML use the controller
####How on HTML

1. Attach the controller to this element
`ng-controller="StoreController as store"`
_"ControllerName as alias"_

2. The product values

HTML
```html

<div class="well" ng-controller="StoreController as store">
  <h1>{{store.product.name}}</h1>
  <h2>{{store.product.type}}</h2>
  <h2>{{store.product.price}}</h2>
  <p>{{store.product.description}}</p>
    <button type="button" class="btn btn-info" ng-show="product.canPurchase">Add to Cart</button>
    <button type="button" class="btn btn-danger" ng-show="!product.canPurchase">Sold Out</button>
</div>

```

More directives
-------------------
####ng-show
Show the button element only if _canPurchase_ is true
  ```html
  <button ng-show="store.product.canPurchase">Add to Cart</button>
  ```

####ng-hide

```html
    <div ng-hide="store.product.soldOut">
        <h1>..</h1>
        <p>...</p>
    </div>
```



Iterating an array
----------------------

####ng-repeat
`ng-repeat="product in store.products"`

```html
<body class="container" ng-controller="StoreController as store">
<!-- Repeats PER div -->
<div class="well" ng-repeat="product in store.products">
  <h1>{{product.name}}</h1>
  <h2>{{product.type}}</h2>
  <h2>{{product.price}}</h2>
  <p>{{product.description}}</p>
  <button type="button" class="btn btn-info" ng-show="product.canPurchase">Add to Cart</button>
  <button type="button" class="btn btn-danger" ng-show="!product.canPurchase">Sold Out</button>
</div>
</body>
```

On app.js
```javascript
(function(){
    var app = angular.module('store', []);
    var guitars = [
        {
            name: 'Stratocaster',
            brand: 'Fender',
            price: 549,
            description: 'Used by Jimi Hendrix',
            canPurchase: true
        },
        {
            name: 'Acoustic(LH)',
            brand: 'Ibanez',
            price: 430,
            description: 'Left Handed acoustic guitar that is made in...',
            canPurchase: false
        }
    ];
    // Controller name : camel case, postfixed : 'Controller'
    app.controller('StoreController', function(){
        // Set properties for the controller
        this.products = guitars;
    });

})();

```

