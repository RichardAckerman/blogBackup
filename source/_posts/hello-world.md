```javascript
angular.js:14199 Error: [$rootScope:inprog] http://errors.angularjs.org/1.5.11/$rootScope/inprog?p0=%24apply
    at angular.js:38
    at n (angular.js:18357)
    at m.$apply (angular.js:18092)
    at customer.js:43
    at dispatch (jquery.min.js:3)
    at q.handle (jquery.min.js:3)
    at m.$scope.exportExcel (customer.js:345)
    at fn (eval at compile (angular.js:15126), <anonymous>:4:224)
    at b (angular.js:16213)
    at e (angular.js:26592)
```
如上错误提示。当用js调用*click()*事件时，提示*Error: [$rootScope:inprog]* 错误。
###原因分析：
```javascript
$scope.$apply();
```
AngularJS报如上错误信息时，代表angular说它已经在处理脏数据了（调用了apply()方法），你别老催他。实际上是脏检查起冲突了。
###解决方法：

```javascript
1.$scope.$applyAsync();
2.$scope.$evalAsync();
3.$timeout(function(){
	// 处理函数
  });
```
