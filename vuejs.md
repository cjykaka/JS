# vuejs
Vue.js是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue采用自底向上增量开发的设计。
## 第一个示例
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Vue Chenjiayao</title>
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>

	<body>
		<!--这是我们的View-->
		<div id="app">
			<p>{{ message }}</p>
			<input type="text" v-model="message"/>
		</div>
		
	</body>
	<script>
		// 这是我们的Model
		var exampleData = {
			message: 'Chenjiayao!'
		}

		// 创建一个 Vue 实例或 "ViewModel"
		// 它连接 View 与 Model
		new Vue({
			el: '#app',
			data: exampleData
		})
	</script>
</html>
```

使用Vue的过程：

    定义View
    定义Model
    创建一个Vue实例或"ViewModel"，它用于连接View和Model

在创建Vue实例时，需要传入一个选项对象，选项对象可以包含数据、挂载元素、方法、模生命周期钩子等等。

在这个示例中，选项对象的el属性指向View，el: '#app'表示该Vue实例将挂载到
```html
<div id="app">...</div>
```
这个元素；
data属性指向Model，data: exampleData表示我们的Model是exampleData对象。
Vue.js有多种数据绑定的语法，最基础的形式是文本插值，使用一对大括号语法，在运行时{{ message }}会被数据对象的
message属性替换，所以页面上会输出"Chenjiayao!"。

在Vue.js中可以使用v-model指令在表单元素上创建双向数据绑定。
```html
<div id="app">
    <p>{{ message }}</p>
    <input type="text" v-model="message"/>
</div>
```
上述的可以将message绑定到文本框，当我们去更改文本框的值时，<p>{{ message }}</p> 中的内容也会被更新。

## Vue.js的常用指令
Vue.js的指令是以v-开头的，它们作用于HTML元素，指令提供了一些特殊的特性，将指令绑定在元素上时，指令会为绑定的目标元素添加一些特殊的行为，我们可以将指令看作特殊

的HTML特性。

Vue.js提供了一些常用的内置指令，接下来我们将介绍以下几个内置指令：
* v-if指令
* v-show指令
* v-else指令
* v-for指令
* v-bind指令
* v-on指令

Vue.js具有良好的扩展性，我们也可以开发一些自定义的指令。

### v-if指令
v-if是条件渲染指令，它根据表达式的真假来删除和插入元素，它的基本语法如下：
```html
v-if="expression"
```
expression是一个返回bool值的表达式，表达式可以是一个bool属性，也可以是一个返回bool的运算式。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Vue Chenjiayao</title>
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>
	<body>
		<div id="app">
			<h1>Welcome!</h1>
			<h1 v-if="yes">Yes!</h1>
			<h1 v-if="no">No!</h1>
			<h1 v-if="age >= 25">Age: {{ age }}</h1>
			<h1 v-if="name.indexOf('Chenjiayao') >= 0">Name: {{ name }}</h1>
		</div>
	</body>
	
	<script>
		var vm = new Vue({
			el: '#app',
			data: {
				yes: true,
				no: false,
				age: 22,
				name: 'Chenjiayao'
			}
		})
        
	</script>
</html>
```

yes, no, age, name这4个变量都来源于Vue实例选项对象的data属性。

这段代码使用了4个表达式：
* 数据的yes属性为true，所以"Yes!"会被输出；
* 数据的no属性为false，所以"No!"不会被输出；
* 运算式age >= 25返回false，所以"Age: 22"不会被输出；
* 运算式name.indexOf('Chenjiayao') >= 0返回true，所以"Name: Chenjiayao"会被输出。

### v-show指令
v-show也是条件渲染指令，和v-if指令不同的是，使用v-show指令的元素始终会被渲染到HTML，它只是简单地为元素设置CSS的style属性。
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Vue ChenJiayao</title>
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>
	<body>
		<div id="app">
			<h1>Welcome!</h1>
			<h1 v-show="yes">Yes!</h1>
			<h1 v-show="no">No!</h1>
			<h1 v-show="age >= 25">Age: {{ age }}</h1>
			<h1 v-show="name.indexOf('ChenJiayao') >= 0">Name: {{ name }}</h1>
		</div>
	</body>
	
	<script>
		
		var vm = new Vue({
			el: '#app',
			data: {
				yes: true,
				no: false,
				age: 47,
				name: 'Kaka'
			}
		})
	</script>
</html>
```

### v-else指令
可以用v-else指令为v-if或v-show添加一个“else块”。v-else元素必须立即跟在v-if或v-show元素的后面——否则它不能被识别。

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>Vue ChenJiayao</title>
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>
	<body>
		<div id="app">
			<h1 v-if="age >= 25">Age: {{ age }}</h1>
			<h1 v-else>Name: {{ name }}</h1>
			<h1> &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp VS</h1>
			<h1 v-show="name.indexOf('Jia') >= 0">Name: {{ name }}</h1>
			<h1 v-else>Sex: {{ sex }}</h1>
		</div>
	</body>

	<script>
		var vm = new Vue({
			el: '#app',
			data: {
				age: 22,
				name: 'ChenJiayao',
				sex: 'Male'
			}
		})
	</script>
</html>
```
v-else元素是否渲染在HTML中，取决于前面使用的是v-if还是v-show指令。这段代码中v-if为true，后面的v-else不会渲染到HTML；v-show为true，但是后面的v-else仍然渲染到HTML了

### v-for指令
