promise-click
==========

### 描述

当点击事件返回为promise，在promise未结束前会为元素添加disabled样式类并失效点击事件，在promise结束后恢复

#### Install

npm i angular-promise-click --save

or

bower i angular-promise-click --save

#### Demo

`example/index.html`

#### Use

```js
var app = angular.module('jsbin', ['angular-promise-click']);
  app.controller('DemoCtrl', function($q) {
    this.name = 'World';
    function xx() {
      this.defered = $q.defer();
      var self = this;
      setTimeout(function() {
        self.defered.resolve('tttt');
      }, 3000);
      return self.defered.promise;
    }
    this.test = function() {
      console.log(123)
      return xx().then(function(result) {
        console.log('test1: ' + result);
        return xx().then(function(r) {
          console.log('test2:' + r);
        })
      });
    }
    this.testConsole = function() {
      console.log('test console');
    }
  });
```

```html
<body ng-app="jsbin">
  <div ng-controller="DemoCtrl as demo">
    <h1>Hello {{demo.name}}</h1>
    <button promise-click="demo.test();demo.testConsole();">test</button>
  </div>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
</body>
```