Forms
======

####ng-model - used to bind form value to a variable in the current controller
- The magic of two-way binding

```html

        <form>
        <p><strong>{{review.stars}} Stars</strong>: {{review.body}}</p>
        <cite>-{{review.author}}</cite>
          <select class="form-control" ng-model="review.stars">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
          <div class="form-group">
            <textarea class="form-control" placeholder="Write a short review of the product" ng-model="review.body"></textarea>
          </div>
          <div class="form-group">
            <input type="email" class="form-control" id="email" placeholder="cee@cee.com" ng-model="review.author">
          </div>
          <button type="submit" class="btn btn-default">Submit</button>
        </form>

```

On textarea
`<textarea class="form-control" placeholder="Write a short review of the product" ng-model="review.body"></textarea>`

Select
`<select class="form-control" ng-model="review.stars">`

Input
`<input type="email" class="form-control" id="email" placeholder="cee@cee.com" ng-model="review.author">`

Checkbox(value is true/false)
`<input ng-model="review.terms">I agree to terms`


`<input ng-model="reviewer.gender" type="radio" value="male">Male`
`<input ng-model="reviewer.gender" type="radio" value="female">Female`


Refactor using a controller
==========================
html
```html

        <form ng-controller="ReviewController as reviewCtrl">
        <p><strong>{{reviewCtrl.review.stars}} Stars</strong>: {{reviewCtrl.review.body}}</p>
        <cite>-{{reviewCtrl.review.author}}</cite>
          <select class="form-control" ng-model="reviewCtrl.review.stars">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
          <div class="form-group">
            <textarea class="form-control" placeholder="Write a short review of the product" ng-model="reviewCtrl.review.body"></textarea>
          </div>
          <div class="form-group">
            <input type="email" class="form-control" id="email" placeholder="cee@cee.com" ng-model="reviewCtrl.review.author">
          </div>
          <button type="submit" class="btn btn-default">Submit</button>
        </form>

```

app.js

```javascript

    app.controller('ReviewController', function(){
        this.review = {};
    });

```
Accepting Form submissions
=========================

####ng-submit - allows us to call a function after the form is submitted

On form:

```html
<form ng-controller="ReviewController as reviewCtrl" ng-submit="reviewCtrl.addReview(product)">
```

On js:
#####Pushing to an array(again data-binding)
#####Clearing a form
```javascript
    app.controller('ReviewController', function(){
        this.review = {};
        this.addReview = function(product){
            product.reviews.push(this.review);
            this.review = {};
        };
    });

```

Form Validations
=====================

1. Turn off default html validations

```html
    <form novalidate>
    ..
    </form>
```

2. Add required to all form controls, and debug 

```html
    <form name="reviewForm" novalidate>
    <input required>
    <!-- true/false if form is valid -->
    <!--  $valid -> angular property of the form -->
    {{reviewForm.$valid}}
    </form>
```

3. Prevent from submitting false values

```html
<form name="reviewForm" ng-controller="ReviewController as reviewCtrl" ng-submit="reviewForm.$valid && reviewCtrl.addReview(product)" novalidate>

```

###On the fly

Before typing angular places these classes on the field
- ng-pristine -> Before typing
- ng-dirty -> after typing
- ng-invalid -> 
- ng-valid ->

For input field colors
======================
Add to css
```css
.ng-invalid.ng-dirty{
    border-color: #FA787E;
}
.ng-valid.ng-dirty{
    border-color: #78FA89;
}

```
