# Passing arguments to tasks

By default, when you call a task, for example:

```js
var method = function (param) {
  console.log("Type of param: '" + (typeof param) + "'. Value:", param);
};

var param = {str: "hello"};
jxcore.tasks.addTask(method, param);
// Type of param: 'object'. Value: { str: 'hello' }
```

the `param` is internally processed with `JSON.stringify()`, sent to task and then parsed back (`JSON.parse()`).

However there are some scenarios, when user already have stringified value and wants to pass it 'as-is', while having it parsed in the task's method.

In that case, the above code would behave differently: `addTask()` would stringify the argument again to parse it back, but at this point it would still be a string, instead of parsed object:

```js
var param = JSON.stringify({str: "hello"});
jxcore.tasks.addTask(method, param);
//Type of param: 'string'. Value: '{"str":"hello"}'
```

Note the `string` type of the `param`.

To avoid this, there are few extra methods available:

* jxcore.tasks._addTask()
* jxcore.tasks._runOnce()
* jxcore.tasks._runOnThread()
* method._runTask()
* method._runOnce()

By using them user avoids default `JSON.stringify()` invocation and receives parsed object into the task:

```js
var param = JSON.stringify({str: "hello"});
jxcore.tasks._addTask(method, param);
// Type of param: 'object'. Value: { str: 'hello' }
```
