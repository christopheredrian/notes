Filters, Directive and Cleaning up code
=======================================

Directives
---------------
###ng-app - attach a module to the page
```html
<!DOCTYPE html>
<html ng-app="store">

</html>
```
###ng-controller - attach a controller to the page
```html
<body ng-controller="StoreController as store">
    
</body>
```
###ng-show/hide - display based on the value of the object
```html
<h1 ng-show="show"></h1>
```
####Show a div if array has value
```html
<!-- This will return 0 if images has no length  -->
<div ng-show="product.images.length">
    
</div>

<!-- I prefer -->
<div ng-show="product.images">
    
</div>
```
###ng-repeat - repeat an array
```html
<li ng-repeat="product in store.products">{{product.name}}</li>
```


##Filtering

`{{data * | filter:options}}` 

```html
<li ng-repeat="product in store.products">Price: {{product.price | currency }}</li>
```

**Some Filters**
####date
`{{ '1232445132' | date:'MM/dd/yyyy @ h:mma'}}`
####uppercase & lowercase
`{{ "string" | uppercase }}`
###limitTo - limits the num of characts
`{{ "stringisthis | limitTo:5"}}`
`<li ng-repeat="product in store.products | limitTo:2">{{product.name}}</li>`
    - to limit the top 2 products
###orderBy
`<li ng-repeat="product in store.products | orderBy:'price'">{{product.name}}</li>` 

**Descending**

`<li ng-repeat="product in store.products | orderBy:'-price'">{{product.name}}</li>`

Loading Images
-------------------
**Putting the url on src will not work** use:

###ng-src
__If images contains an array__
```html
<img ng-src="{{product.images[0]}}"/>
```

__To display all images sequentially__
```html
<img ng-repeat="image in product.images" ng-src="{{image}}"/>
```

or use an `<li>`
```html
<li ng-repeat="image in product.images">
    <img ng-src="{{image}}"/>
</li>
```

__On app.js__
```javascript
var guitars = [
    {
        name: 'Stratocaster',
        brand: 'Fender',
        price: 549,
        description: 'Used by Jimi Hendrix',
        canPurchase: true,
        images:[
            'img/strat1.jpg',
            'img/strat2.jgp',
            'img/start3.jpg'
        ]
    }
];
```

__If images contains an object__

```html
<img class="thumb img-rounded pull-right" ng-src="{{product.images.thumb}}">
```

__The Data(on app.js)__
```javascript
var guitars = [
    {
        name: 'Stratocaster',
        brand: 'Fender',
        price: 549,
        description: 'Used by Jimi Hendrix',
        canPurchase: true,
        images: {
            thumb: 'img/strat.jpg',
            full: ''
        }
    }
];

```





Context
---------------
**app.js**

```javascript
(function(){
    var app = angular.module('store', []);
    var guitars = [
        {
            name: 'Stratocaster',
            brand: 'Fender',
            price: 549,
            description: 'Used by Jimi Hendrix',
            canPurchase: true,
            images: {
                thumb: 'img/strat.jpg',
                full: ''
            }
        },
        {
            name: 'Acoustic(LH)',
            brand: 'Ibanez',
            price: 430,
            description: 'Left Handed acoustic guitar that is made in...',
            canPurchase: false
            ,
            images: {
                thumb: 'img/lhIbanez.jpg',
                full: ''
            }
        }
    ];
    // Controller name : camel case, postfixed : 'Controller'
    app.controller('StoreController', function(){
        // Set properties for the controller
        this.products = guitars;
    });

})();

```


Tabs
------------

###ng-init (Only use in prototyping)
_Allows us to initialize variables_
 **section or div**
`<section ng-init="tab = 1">`

###ng-class - adds a class to element
    - Accepts an object 
    - `ng-class={active: true}`
sets the highlighted tab
`ng-class="{ active:tab === 1}`
- If tab === 1 
- Appennds: active: true to the class

###ng-click - triggers the value when the element is clicked
`tab = 1` 
_Two way data binding - expressions are re-evaluated when properties change_

```html
    <ul class="nav nav-pills">
      <li><a href ng-click="tab = 1">Description</a></li>
      <li><a href ng-click="tab = 2">Shipping Information</a></li>
    </ul>
    {{tab}}
```

####Code for tabs

```html
    <section ng-init="tab = 1">
      <ul class="nav nav-pills">
        <li ng-class="{ active:tab === 1}">
         <a href ng-click="tab = 1">Description</a>
        </li>
        <li ng-class="{ active:tab === 2}">
          <a href ng-click="tab = 2">Shipping Information</a>
        </li>
      </ul>
      <div  class="panel well" ng-show="tab === 1">
        <h4>Product Details:</h4>
        <p class="">{{product.description}}</p>
      </div>
      <div  class="panel well" ng-show="tab === 2">
        <h4>Shipping Information</h4>
        <p>Ships from: {{product.shippingFrom}}</p>
      </div>
    </section>


```

Cleaning Our code(Tabs) using another Controller
-------------------------------------------------
- Create a new controller in this case PanelController
- Move init to js
- Remove `ng-click` add a function instead

HTML

```html
   <section ng-controller="PanelController as panel" ng-init="tab = 2">
      <ul class="nav nav-pills">
        <li ng-class="{ active:panel.isSelected(1)}">
         <a href ng-click="panel.selectTab(1)">Description</a>
        </li>
        <li ng-class="{ active:panel.isSelected(2)}">
          <a href ng-click="panel.selectTab(2)">Shipping Information</a>
        </li>
      </ul>
      <div  class="panel well" ng-show="panel.isSelected(1)">
        <h4>Product Details:</h4>
        <p class="">{{product.description}}</p>
      </div>
      <div  class="panel well" ng-show="panel.isSelected(2)">
        <h4>Shipping Information</h4>
        <p>Ships from: {{product.shippingFrom}}</p>
      </div>
    </section>
```

Javascript Controller

```javascript
    app.controller('PanelController', function(){
        this.tab = 1;
        this.selectTab = function(setTab){
            this.tab = setTab;
        };
        this.isSelected = function(checkTab){
            return this.tab === checkTab;
        }
    });

```