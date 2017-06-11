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

### v-model
单选按钮:
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Vue 单选</title>
        <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
    </head>
    <body>
        <div id="app">
            <h1>欢迎选择你的课程!</h1>
            <input type="radio" id="js" value="跨平台脚本" v-model="picked">
            <label for="js">跨平台脚本</label>
        <br>
            <input type="radio" id="java" value="面向对象程序设计" v-model="picked">
            <label for="java">面向对象程序设计</label>
        <br>
            <input type="radio" id="Android" value="安卓UI设计" v-model="picked">
            <label for="Android">安卓UI设计</label>
        <br>
        <span>选择的课程为: {{ picked }}</span>
        </div>
   </body>
    <script>
        new Vue({
        el: '#app',
        data: {
	    picked : '当前无'
            }
        })
    </script>
    
</html>
```

复选框：
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Vue 复选框</title>
        <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
    </head>
    <body>
        <div id="app">
	  <h1>欢迎选择你的课程!</h1>
            <input type="checkbox" id="js" value="跨平台脚本" v-model=" checkedNames">
            <label for="js">跨平台脚本</label>
        <br>
            <input type="checkbox" id="java" value="面向对象程序设计" v-model=" checkedNames">
            <label for="java">面向对象程序设计</label>
        <br>
            <input type="checkbox" id="Android" value="安卓UI设计" v-model=" checkedNames">
            <label for="Android">安卓UI设计</label>
        <br>
        <span>选择的课程为: {{  checkedNames }}</span>
        </div>
    </body>
    <script>
        new Vue({
        el: '#app',
        data: {
        checkedNames: []
            }
        })
    </script>
</html>
```

select列表
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Vue 列表</title>
        <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
</head>
    <body>
    <div id="app">
        <select v-model="selected" name="course">
            <option value="">选择一门课程</option>
            <option value="js">跨平台脚本</option>
            <option value="java">面向对象程序设计</option>
            <option value="Android">安卓UI设计</option>
        </select>
 
        <div id="output">
            选择的课程是: {{selected}}
        </div>
    </div>
    </body>
    
    <script>
        new Vue({
        el: '#app',
        data: {
	    selected: '' 
  }
})
    </script>
</html>
```

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
			<p v-if="yes">Are you ok?</p>
			<p v-if="no">I am fine!</p>
			<p v-if="age >= 25">Age: {{ age }}</p>
			<p v-if="name.indexOf('Chenjiayao') >= 0">Name: {{ name }}</p>
		</div>
	</body>
	
	<script>
		
		var vm2 = new Vue({
			el: '#app',
			data: {
				yes: true,
				no: false,
				age: 28,
				name: 'Chenjiayao'
			}
		})
	</script>
</html>
```

yes, no, age, name这4个变量都来源于Vue实例选项对象的data属性。

这段代码使用了4个表达式：
* 数据的yes属性为true，所以"Are you ok?"会被输出；
* 数据的no属性为false，所以">I am fine!"不会被输出；
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

v-for指令基于一个数组渲染一个列表，它和JavaScript的遍历语法相似：

v-for="item in items"

items是一个数组，item是当前被遍历的数组元素。

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>Vue Chenjiayao</title>
		<link rel="stylesheet" href="styles/demo.css" />
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>

	<body>
		<div id="app">
			<table>
				<thead>
					<tr>
						<th>姓名</th>
						<th>号码</th>
						<th>球队</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="person in people">
						<td>{{ person.name  }}</td>
						<td>{{ person.num  }}</td>
						<td>{{ person.team  }}</td>
					</tr>
				</tbody>
			</table>
		</div>
	</body>
	<script>
		var vm = new Vue({
			el: '#app',
			data: {
				people: [{
					name: 'C罗纳尔多',
					num: 7,
					team: '皇家马德里'
				}, {
					name: '贝尔',
					num: 11,
					team: '皇家马德里'
				}, {
					name: '梅西',
					num: 10,
					team: '巴塞罗那'
				}, {
					name: '诺伊尔',
					num: 1,
					team: '拜仁慕尼黑'
				}]
			}
		})
	</script>

</html>
```
在选项对象的data属性中定义了一个people数组，然后在#app元素内使用v-for遍历people数组，输出每个person对象的姓名、号码和球队。

### v-on指令
事件监听可以使用 v-on 指令：

v-on指令用于给监听DOM事件，例如监听<a>元素的点击事件：
```html
<a v-on:click="doSomething">
```

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Vue ChenJiayao</title>
        <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
    </head>
    <body>
        <div id="app">
            <button v-on:click="counter += 1">增加 1</button>
            <p>这个按钮被点击了 {{ counter }} 次。</p>
        </div>

    </body>
    
    <script>
        new Vue({
        el: '#app',
        data: {
        counter: 0
        }
        })
    </script>
</html>
```




