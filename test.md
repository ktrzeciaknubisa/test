### removeColors(txt)

Removes from `txt` string all formatting control codes and returns a new string.

```js
// [31mformatted with red [39m
var formatted = jxcore.utils.console.setColor("formatted with red", "red");

// formatted with red
var plain = jxcore.utils.console.removeColors(formatted);
```
