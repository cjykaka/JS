# vuejs
Vue.js是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue采用自底向上增量开发的设计。
## 第一个示例
Vue.js 的核心是一个允许采用简洁的模板语法来声明式的将数据渲染进 DOM

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
        <h1>姓名：{{ Name }}</h1>
        <h1>年龄：{{ Age }}</h1>
        <h1>学校：{{ School }}</h1>
    </div>

    <script>
    //Model
    var kk = {
        Name: '陈家耀',
        Age: 22,
        School:'浙江大学城市学院',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: kk,
    });
   
    </script>
</body>
```
这个的Model就是kk变量，而ViewModel就是这里的new Vue()得到的对象。

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
Vue 在背后做了大量工作。现在数据和 DOM 已经被绑定在一起，所有的元素都是响应式的。

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
v-model可用于一些表单元素,常见的input,checkbox,radio,select: 
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

综合
```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>Vue Chenjiayao</title>
		<script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
	</head>

	<body>
	

<div id="app">
    <form>
        姓名：
        <input type="text" v-model="abc.name" placeholder="姓名"/>
        <br />
        性别：
        <input type="radio" id="one" value="One" v-model="abc.sex"/>
        <label for="man">男</label>
        <input type="radio" id="two" value="Two" v-model="abc.sex"/>
        <label for="male">女</label>
        <br />
        兴趣爱好：
        <input type="checkbox" id="jack" value="book" v-model="abc.interest"/>
        <label for="jack">阅读</label>
        <input type="checkbox" id="john" value="swim" v-model="abc.interest"/>
        <label for="john">游泳</label>
        <input type="checkbox" id="move" value="game" v-model="abc.interest"/>
        <label for="move">游戏</label>
        <input type="checkbox" id="mike" value="song" v-model="abc.interest"/>
        <label for="mike">唱歌</label>
        <br />
        年级：
        <select v-model="abc.identity">
            <option value="1" selected>大一</option>
            <option value="2">大二</option>
            <option value="3">大三</option>
            <option value="4">大四</option>
        </select>          
    </form>
</div>
<script >
    new Vue({
        el: '#app',
        data: {
            abc:{
                name:'',
                sex:'',
                interest:[],
                identity:''
            }
        }
    })
</script>


```

## Vue.js的常用指令
Vue.js的指令是以v-开头的，它们作用于HTML元素，指令提供了一些特殊的特性，将指令绑定在元素上时，指令会为绑定的目标元素添加一些特殊的行为，我们可以将指令看作特殊

的HTML特性。

Vue.js提供了一些常用的内置指令，接下来我们将介绍以下几个内置指令：
* v-if指令
* v-show指令
* v-else指令
* v-for指令
* v-once指令
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
		<title>Vue If</title>
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>
	<body>
		<div id="app">
			<h1>Welcome!</h1>
			 <h1>姓名：<label v-text="Name"></label></h1>
        	 <h1>是否毕业：<span v-if="IsBy">是</span></h1>
        	 <h1>是否及格：<span v-if="Score>60">合格</span><span v-else>不及格</span></h1>
			 <h1>年龄：<span v-if="age >= 25">{{ age }}</span></h1>
        	 <h1>学校：{{ School }}</h1>
		</div>
	</body>
	
	<script>
		
		var vm2 = new Vue({
			el: '#app',
			data: {
				Name: '陈家耀',
        		IsBy: true,
        		Score: 80,
				age: 22,
        		School:'浙江大学城市学院'
			}
		})
	</script>
</html>
```

IsBy, Score, age 这3个变量都来源于Vue实例选项对象的data属性。

* 数据的Isby属性为true，所以"是"会被输出；
* 数据的Score属性为rue，所以"80"会被输出；
* 运算式age >= 25返回false，所以"Age: 22"不会被输出；

注意：v-if指令是根据条件表达式的值来执行元素的插入或者删除行为。
这一点可以从渲染的HTML源代码看出来，v-if值为false的元素没有渲染到HTML。

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
			 <h1>姓名：<label v-text="Name"></label></h1>
        	 <h1>是否毕业：<span v-show="IsBy">是</span></h1>
        	 <h1>是否及格：<span v-show="Score>60">合格</span><span v-else>不及格</span></h1>
			 <h1>年龄：<span v-show="age >= 25">{{ age }}</span></h1>
        	 <h1>学校：{{ School }}</h1>
		</div>
	</body>
	
	<script>
		
		var vm = new Vue({
			el: '#app',
			data: {
				Name: '陈家耀',
        		IsBy: true,
        		Score: 80,
				age: 22,
        		School:'浙江大学城市学院'
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
		
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>

    <body>
        <div id="app">
            <ul>
            <li v-for="value in nums">{{value}}</li>
            </ul>
        </div>
    </body>
    <script>
    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: {
            nums: [1, 2, 3, 4, 5, 6, 7, 8, 9]
        }
    });
    </script>
</html>

```

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
          <ol>
            <li v-for="todo in todos">
             {{ todo.text }}
           </li>
         </ol>
       </div>
	</body>
	<script>
		var kk = new Vue({
        el: '#app',
        data: {
        todos: [
        { text: '学习 JavaScript' },
        { text: '学习 Vue' },
        { text: '答辩' }
             ]
            }
        })
    </script>

</html>
```


在控制台里，输入 kk.todos.push({ text: '新项目' })，你会发现列表中添加了一个新项。


### v-once指令
v-once表示只渲染元素和组件一次。随后的重新渲染,元素/组件及其所有的子节点将被视为静态内容并跳过。
```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>Vue Chenjiayao</title>
		
		<script src="https://unpkg.com/vue/dist/vue.js"></script>
	</head>
    <div id="app">
        <h1>姓名：<label v-once v-text="Name"></label></h1>
        <h1 v-once>年龄：{{ Age }}</h1>
        <h1>学校：{{ School }}</h1>
    </div>
    <script>
    //Model
    var data = {
        Name: '陈家耀',
        Age: 22,
        School:'浙江大学城市学院',
    }

    //ViewModel
    var vue = new Vue({
        el: '#app',
        data: data,
    });
    </script>
</html>
```
只要使用v-once指令的，View和Model之间除了初次渲染同步，之后便不再同步，而同一次绑定里面没使用v-once指令的还是会继续同步。



### v-on指令
属性jquery的朋友应该很熟悉这个“on”，对于时间的监听和绑定，jquery里面最常用的就是on了。同样，在Vue里面，v-on指令用来绑定标签的事件

```html
v-on:event="expression";
```
这里的event可以是Javascript里面的常用事件，也可以是自定义事件。

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

除了直接在标签内写处理逻辑，还可以定义方法事件处理器：
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Vue on</title>
        <script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
    </head>


    <div id="app">
            <h1>姓名：<label v-text="Name"></label></h1>
            <h1>年龄：{{ Age }}</h1>

            <button class="btn btn-primary" v-on:click="Hello">Hello</button>
        </div>
        <script>
        //Model
        var data = {
            Name: '陈家耀',
            Age: 22,
        }

        //ViewModel
        var vue = new Vue({
            el: '#app',
            data: data,
            methods: {
                Hello: function (event) {
                    // `this` 在方法里指当前 Vue 实例
                    alert('Hello ' + this.Name + '!');
                    this.Age++;
                }
            }
        });
        </script>
</html>
```



