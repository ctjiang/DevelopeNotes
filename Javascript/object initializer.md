# Object Initiaizer
Object initializer是用在初始化Javascript物件的運算式，物件最外層以大括號為界，property之間用逗點分隔，
property的key和value間則以冒號隔開。key是property的名稱，而value則可以是javascript的原生型別或其它的物件。

其基本的語法為：
```
o = {
  a: "foo",
  b: 42,
  c: {},
  1: "number literal property",
  "foo:bar": "string literal property",

  shorthandProperty,

  method(parameters) {
    // …
  },

  get property() {},
  set property(value) {},

  [expression]: "computed property",

  __proto__: prototype,

  ...spreadProperty,
};

```
## Object literal syntax vs. JSON
雖然Object literal語法和JSON (JavaScript Object Notation)非常相似，但是有其基本上的差異：
* JSON只能用語法```"property": value```定義property，名稱部份要用雙引號標記，不可使用shortname的格式，也不能使用computed property name。
* JSON的property value只能用字串，數字，true，false，null，array或其它的JSON物件。這表示JSON無法使用method或非plain的物件(如Date或RegExp)。
* 在JSON中，```__proto__```是正規的property key，而在Javascript物件literal中，會用來設定物件的prototype
JSON是object literal syntax的嚴格子集，這表示合法的JSON文字可以parse成object literal不會引發語法錯誤。唯一的例外是object literal禁用```__proto__```當成property key，但```JSON.parse()```會視為一般的property。
