# GraphQL
## 工作机制
一个GraphQL查询可以包含一个或者多个操作（operation）。操作（operation）可以使两种类型：查询（Query）或者修改（mutation）。

example1：
```
query {
  client(id: 1) {
    id 
    name
  }
}
```
上面的例子有三个不同的部分组成:
* client是查询的operation
* (id: 1)包含了传入给Query的参数
* 查询包含id和name字段，这些字段也是我们希望查询可以返回的

server给这个查询返回：
```
{
  "data": {
    "client": {
      "id": "1",
      "name": "Chenjiayao"
    }
  }
}
```

example2：
```
query {
  products(product_category_id: 1, order: "price DESC") {
    name 
    shell_size
    manufacturer
    price
  }
}
```
这次我们查询products，并传入两个参数：product_category_id用于过滤，一个指明按照price字段降序排列。查询中包含的字段是：name、shell_size、manufacturer和price）。

返回的结果：
```
{
  "data": {
    "products": [
      {
        "name": "Mapex Black Panther Velvetone 5-pc Drum Shell Kit",
        "shell_size": "22\"x18\" Bass Drum, 10\"x8\" & 12\"x9\" Toms, 14\"x14\" & 16\"x16\" Floor Toms",
        "manufacturer": "Mapex",
        "price": 2949.09
      },
      {
        "name": "Pearl MCX Masters Natural Birdseye Maple 4pc Shell Pack with 22\" Kick",
        "shell_size": "22x18\" Virgin Bass Drum 10x8\" Rack Tom 12x9\" Rack Tom 16x16\" Floor Tom",
        "manufacturer": "Pearl",
        "price": 1768.33
      }
    ]
  }
}
```
从这几个初级的例子里你可以看出来GraphQL允许客户端明确指定它要的是什么，避免了数据后去的冗余或者不足。

GraphQL是很好的查询语言。所有的operation、参数和所有可以查询的字段都需要在GraphQL server上定义、实现。
## Fragments

现在，客户端APP要获取另个分开的list： drum sets和cymbals。在GraphQL里你不会被限制在一个operation里。
```
query {
  drumsets: product(product_category_id: 1) {
    id
    name
    manufacturer
    price
    pieces
    shell_size
    shell_type
  }

  cymbals: products(product_category_id: 2) {
    id
    name
    manufacturer
    price
    cymbal_size
  }
}
```
在查询的两个对象中都包含了字段：id、name、manufacturer、price。

为了避免重复字段，我们可以使用GraphQL提供的Fragments。我们来把重复的字段都提出来，放到一个fragment里：
```
query {
  drumsets: products(product_category_id: 1) {
    ...ProductCommonFields
    prices
    shell_size
    shell_type
  }

  cymbals: products(product_category_id: 2) {
    ...ProductCommonFields
    cymbal_size
  }
}

fragment ProductCommonFields on Product {
  id
  name
  manufacturer
  price
}
```
要使用一个Fragment就使用操作符：...。

## 变量（Variable）

我们要尽量减少查询语句中的重复：
```
client(id: 1) {
  name
  dob
}

purchasses(client_id: 1) {
  date
  quantity
  total
  product {
    name 
    price
    product_category {
      name
    }
  }
  client {
    name 
    dob 
  }
}
```
我们使用两个operation查询server，并且每个都包含了client_id参数。我们可以使用GraphQL的变量集中在一起。我们可以添加一个clientID变量。
```
query($clientId: Int) {
  client(id: $clientId) {
    name
    dob
  }

  purchases(client_id: $clientId) {
    date
    quantity
    total
    product {
      name
      price
      product_category {
        name
      }
    }
    client {
      name
      dob
    }
  }
}
```
我们在operation的前面定义了变量，然后我们就可以在整个查询中使用这个变量了。 为了使用变量的定义，我们需要在查询的时候附带变量值的JSON。

{
  "clientId": 1
}

当然，我们也可以指定一个默认值：
```
query ($date: String = "2017/06/10") {
  purchases(date: $date) {
    date
    quantity
    total
  }
}
```

## Mutation（修改）

GraphQL不仅可以用来查询数据，也可以创建、更新和销毁数据。当然和查询一样，这些也需要server端有对应的实现。增、删、改一类的operation在GraphQL里统称为Muration（修改）。
```
mutation {
  create_client (
    name: "陈家耀"
    dob: "2017/06/10"
  ) {
    id 
    name
    dob
  }
}
```
我们现在指定operation的类型为mutation，而不是query。在create_client操作里我们传入了创建一个client需要的数据，并最终返回一个查询集合：
```
{
  "data": {
    "create_client": {
      "id": "5",
      "name": "陈家耀",
      "dob": "2017/06/10"
    }
  }
}
```
上面的数据有一点错误，生日不对。下面就来用更新来fix这个错误：
```
mutation {
  update_client (
    id: 5
    dob: "1995/06/10"
  ) {
    id
    name
    dob
  }
}
```
最后，如果我们要删除这个数据可以这样：
```
mutation {
  destroy_client(id: 5) {
    name 
    dob
  }
}
```
