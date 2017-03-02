[slide]
# window平台安装-mongodb
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-download.jpg"/>
[slide]
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/win-install1.jpg" />
[slide]
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/win-install2.jpg" />
[slide]

# MongoDB 数据库的概念
* 在mongodb中基本的概念是文档、集合、数据库
* 下表将帮助您更容易理解Mongo中的一些概念
<img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-jieGou-1.png">

[slide]
* 通过下图实例，我们也可以更直观的的了解Mongo中的一些概念：

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/Figure-1-Mapping-Table-to-Collection-1.png"></p>

[slide]
# <h4>数据库</h4>
* <h6>1、一个mongodb中可以建立多个数据库。</h6>
* <h6>2、MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。</h6>
* <h6>3、数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。</h6>

 ```
 1.不能是空字符串（"")。
2.不得含有' '（空格)、.、$、/、\和\0 (空宇符)。
3.应全部小写。
4.最多64字节。
```
[slide]
* 4、有一些数据库名是保留的，可以直接访问这些有特殊<br>
作用的数据库。
```
1.admin： 从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数
据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个
数据库运行，比如列出所有的数据库或者关闭服务器。
2.local: 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
3.config: 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的
相关信息。
```
[slide]
# <h5>二、文档</h5>

* <h6>文档是mongodb中的最核心的概念，是其核心单元，我们可以将文档类比成关系型数据库中的每一行数据。</h6>

* <h6>多个键及其关联的值有序的放置在一起就是文档。MongoDB使用了BSON这种结构来存储数据和网络数据交换。</h6>

* <h6>BSON数据可以理解为在JSON的基础上添加了一些json中没有的数据类型。</h6>

[slide]

* <h6>如果我们会JSON，那么BSON我们就已经掌握了一半了，至于新添加的数据类型后面我会介绍。</h6>

* <h4>文档例子如下：</h4>
```
{name:"张三",age:20,hobby:["看书","旅游","唱歌"]}
```
[slide]
* <h2>需要注意的是：</h2>

* <h4>1. 文档中的键/值对是有序的。</h4>

* <h4>2. 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌人的文档)。</h4>

* <h4>3. MongoDB区分类型和大小写。</h4>

* <h4>4. MongoDB的文档不能有重复的键。</h4>

* <h4>5. 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。</h4>
[slide]

* <h2>文档键命名规范：</h2>

* <h4>1 键不能含有\0 (空字符)。这个字符用来表示键的结尾。</h4>

* <h4>2 .和$有特别的意义，只有在特定环境下才能使用。</h4>

* <h4>3 以下划线"_"开头的键是保留的(不是严格要求的)。</h4>

[slide]
# <h1>三、集合</h1>

* <h4>集合就是一组文档的组合。如果将文档类比成数据库中的行，那么集合就可以类比成数据库的表。</h4>

* <h4>在mongodb中的集合是无模式的，也就是说集合中存储的文档的结构可以是不同的，比如下面的两个文档可以同时存入到一个集合中：</h4>
[slide]

```
{"name":"mengxiangyue"}
{"Name":"mengxiangyue","sex":"nan"}
注：当第一个文档插入时，集合就会被创建。

```
[slide]
# <h6>合法的集合名</h6>

* <h6>1. 集合名不能是空字符串""。</h6>

* <h6>2. 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。</h6>

* <h6>3. 集合名不能以"system."开头，这是为系统集合保留的前缀。</h6>

* <h6>4.用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。　</h6>

[slide]
# <h1>四、 MongoDB 数据类型</h1>

* <h4>下表为MongoDB中常用的几种数据类型。</h4>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-shuJuLeiXing-1.png"></p>
[slide]
# mongodb服务的启用"
* <h5>1-找到mongodb安装目录-按下shift-鼠标右键-选择" <code>在此处打开命令窗口</code></h5>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-1.png" class="img-responsive">

[slide]
* <h6> 2.命令窗体中输入<br> <code>mongod --dbpath=D:\Mongodb\data</code> <br>按回车键</h6>
* <code>注： --dbpath后的值表示数据库文件的存储路径 而且后面的路径必须存在否则服务开启失败</code>
[slide]
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-2.png" class="img-responsive">
[slide]
* <code>注意：这个命令窗体不能关  关闭这个窗口就相当于停止了mongodb服务</code>
[slide]
#<h6>cmd-连接本地mongodb数据库</h6>
* 1-找到mongodb安装目录-按下shift-鼠标右键-选择<code>在此处打开命令窗口</code>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-1.png" />

[slide]
* 2.命令窗体中输入 <code>mongo --host=127.0.0.1</code><br>
   或者 <code>mongo</code> 按回车键
<code>注：--host后的值表示服务器的ip地址</code>

<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-4-1.png" class="img-responsive">
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-4.png" class="img-responsive">

[slide]
* 备注： <code>--host=127.0.0.1</code> 表示的就是本地数据库 <code>每次数据库都会默认连接test数据库</code>
[slide]
# <h6>CMD 连接远程服务器上的mongodb数据库</h6>
* <h6>1.找到mongodb安装目录 按下Shift+鼠标右键 选择 <code>在此处打开命令窗口</code></h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-1.png" class="img-responsive">
[slide]
* <h6>2.命令窗体中输入 <code>mongo --host=123.57.143.189.</code> 按回车键</h6>
* <code>注：--host后的值表示服务器的ip地址</code>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-5.png" class="img-responsive">
[slide]
* 备注： <code>--host=123.57.143.189</code> 表示连接ip是123.57.143.189服务器上的mongodb数据库 <code>每次数据库都会默认连接test数据库</code></p>
[slide]
# <h6>MongoDB 创建数据库</h6>
* <h6>语法结构</h6>
<pre><code>use database_name      database_name代表数据库的名字
注：如果数据库不存在，则创建数据库，否则切换到指定数据库
</code></pre>
[slide]
# <h6>实例</h6>
* <h6>以下实例我们创建了数据库 person:</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-8.png" class="img-responsive">
[slide]
# <h6>MongoDB查看所有数据库</h6>
* <h6>语法结构</h2>
<pre><code>show dbs
注：我们刚创建的数据库 person 如果不在列表内， 要显示它，<br>我们需要向 person 数据库插入一些数据<br> db.person.insert({name:"zhangSan",age:30})
</code></pre>
[slide]
# <h6>实例</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-7.png" class="img-responsive">
[slide]
# <h6>MongoDB查看当前使用的数据库</h6>
* <h6>语法结构</h6>
<pre><code>db 或 db.getName()  
注：db代表的是当前数据库 也就是person这个数据库
</code></pre>

[slide]
<h2><a href="#实例" name="实例" id="实例" class="anchor"></a>实例</h2>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-9.png" class="img-responsive">

[slide]
# <h6>MongoDB 删除数据库</h6>
* <h6>语法结构</h2>
<pre><code>db.dropDatabase()
</code></pre>
[slide]
* <h6>实例</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-shanChuShuJuKu-1.png" class="img-responsive">

[slide]
# <h6>MongoDB 断开与mongodb服务的连接</h6>
* <h6>语法结构</h6>
<pre><code>exit  
</code></pre>

[slide]
# <h6>实例</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-10.png" class="img-responsive">

[slide]
* MongoDB 查看命令api</h1>
* <h6>语法结构</h6>
<pre><code>help   
</code></pre>

[slide]
# <h6>实例</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-6.png" class="img-responsive">
[slide]
# <h6>操作集合方法</h6>

* <h6>查看帮助api</h6>

* <h4>语法</h4>

<pre>db.worker.help()
</pre>

[slide]
# <h6>实例</h6>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-13.png"></p>

[slide]
# <h2>查看当前数据库下有哪集合（collection）</h2>
* <h4>语法</h4>
<pre>show collections
</pre>

[slide]
<h4>实例</h4>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-11.png"></p>

[slide]
* <h6>创建集合（collection）</h6>

* <h6>1. 使用 <code>db.createCollection(collection_Name)</code>方法</h6>

[slide]
* <h6>语法</h6>

<pre><code>db.createCollection("collection_Name")</code><br>     collection_Name集合的名称
</pre>

* <h6>2. 使用 db.collection_Name.insert(document)方法</h6>

* <h6>语法</h6>

<pre><code>db.collection_Name.insert(document)</code><br>
collection_Name集合的名称   document要插入的文档
</pre>

[slide]

<h4>实例</h4>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-14.png"></p>
[slide]

<pre>注：两者的区别在于前者创建了一个空的worker集合 后者创建了一个空的worker<br>集合并添加了一个Document数据
</pre>
[slide]
* <h2>删除当前数据库中的集合（collection）</h2>

* <h4>语法</h4>

<pre><code>db.collection_Name.drop()</code>    collection_Name 集合的名称
</pre>
[slide]
* <h4>实例</h4>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-12.png"></p>



[slide]
# <h6>插入文档</h6>
* <h6>1、 使用insert()方法插入文档</h6>
* <h6>语法</h6>
<pre><code>db.collection_name.insert(document) <br>   collection_name集合的名字    document插入的文档
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.insert({name:'zpx',age:6})<br> 向worker集合添加一个{name:'zpx',age:6}的Document
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-15.png" class="img-responsive">

[slide]
<pre><code>db.worker.insert([{name:'wangWu',age:50},{name:'xiaoMing',age:60}]) <br>向worker集合添加多个[{name:'wangWu',age:50},{name:'xiaoMing',age:60}] 的Documen
</code></pre>

[slide]
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-15-1.png" class="img-responsive">
[slide]
* <h6>2-使用save-方法插入文档" </h6>
* <h6>语法</h6>
<pre><code>db.collection_name.save(document) <br>  collection_name集合的名字 <br>   document插入的文档
注：如果不指定 _id 字段 save() 方法类似于 insert() 方法。<br>如果指定 _id 字段，则会更新该 _id 的数据。
</code></pre>

[slide]
* <h6>实例</h6>
<pre><code>db.person.save({name:"xiaoHong",age:50})
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-1.png" class="img-responsive">
<pre><code>db.person.save({_id:ObjectId("562c9caf671c978b6596e825"),<br>name:"xiaoHong",age:10})
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-2.png" class="img-responsive">


[slide]
# <h6>MongoDB 更新文档</h6>

* <h6>1.update()方法用于更新已存在的文档</h6>

* <h6>语法</h6>

<pre><code>db.collection.update(
   &lt;query&gt;,
   &lt;update&gt;,
   {
     upsert: &lt;boolean&gt;,
     multi: &lt;boolean&gt;,
     writeConcern: &lt;document&gt;
   }
  );</code></pre>

[slide]
* <h4>参数说明：</h4>
<pre><code>query : update的查询条件，类似sql update查询内where后面的。
update : update的对象和一些更新的操作符（如$set,$inc...）等<br> $inc在原基础上累加后更新   $set直接更新
upsert  : 可选，这个参数的意思是，如果不存在update的记录，<br>是否插入objNew,true为插入，默认是false，不插入。
multi  : 可选，mongodb 默认是false,只更新找到的第一条记录，<br>如果这个参数为true,就把按条件查出来多条记录全部更新。
writeConcern  :可选，抛出异常的级别。
</code>
</pre>

[slide]
<h4>实例</h4>

<pre><code>db.worker.update({name:'liSi'},{$set:{name:'liSi_update'}}) </code><br>将document数据中name是liSi 的数据的name修改为liSi_update
注：如果有多条name是liSi的数据只更新一条
</pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-18.png"></p>
[slide]

<pre><code>db.worker.update({name:'liSi_update'}, <br>{$set: {age:40}},{multi:true}) <br>将document数据中name是liSi_update 的数据的age修改为 40
注：如果有多条name是liSi的数据这些数据全部更新</code>
</pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-18-2.png"></p>

[slide]

<pre><code>db.worker.update({name:'liSi_update'},<br>{$inc:{age:1}}) <br>将document数据中name是lliSi_update 的数据的age在原来的基础上加1</code>
</pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-18-1.png"></p>
[slide]
* <h6>2.save()方法通过传入的文档来替换已有文档</h6>
* <h6>语法</h6>

<pre><code>db.collection.save(
&lt;document&gt;,
{
writeConcern: &lt;document&gt;
})
</code>
</pre>
[slide]
<h6>参数说明：</h6>
<pre>  document : 文档数据。
  writeConcern  :可选，抛出异常的级别。
</pre>
[slide]

<h4>实例</h4>

<pre><code>db.person.save({_id:ObjectId("562c9caf671c978b6596e825"),<br>name:"xiaoHong",age:10})
</code>
</pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-2.png"></p>


[slide]
# <h6>MongoDB 删除文档</h6>
* <h6>remove()方法是用来移除集合中的数据。</h6>

<pre><code>注：在执行remove()函数前先执行find()命令来判断<br>执行的条件是否正确，这是一个比较好的习惯。</code>
</pre>

[slide]
# <h6>语法</h6>

<pre><code>db.collection.remove(
   &lt;query&gt;,
   &lt;justOne&gt;
)
如果你的 MongoDB 是 2.6 版本以后的，语法格式如下：
db.collection.remove(
   &lt;query&gt;,
   {
     justOne: &lt;boolean&gt;,
     writeConcern: &lt;document&gt;
   }
)
</code>
</pre>

[slide]
<h6>参数说明：</h6>
<pre>query :（可选）删除的文档的条件。
justOne : （可选）如果设为 true 或 1，则只删除一个文档。
writeConcern  :（可选）抛出异常的级别。
</pre>


[slide]
<h6>实例</h6>

<pre><code>db.worker.remove({name:'fJianZhou'})<br> 删除worker集合里name是fJianZhou的所有Document数据
</code></pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-19.png"></p>
[slide]
<pre><code>db.person.remove({name:"xiaoHong"},1) <br> 删除person集合里name是xiaoHong的第一条数据
</code></pre>

<p><img alt="" src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-shanChuShuJu-1.png"></p>


[slide]
# <h6>MongoDB 查询文档</h6>
* <h6>1.find()方法</h6>
* <h6>语法</h6>
<pre><code>db.collection_name.find()  collection_name 集合的名字
</code></pre>

[slide]
<h6>实例</h6>
<pre><code>db.worker.find()  查询worker下所有的document数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16.png" class="img-responsive">
[slide]
* <h6>2.find()方法 查询指定列</h6>
* <h6>语法</h6>
<pre><code>db.collection_name.find({queryWhere},{key:1,key:1})<br> collection_name 集合的名字 key要显示字段<br>  1表示显示  queryWhere参阅查询条件操作符
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({},{age:1}) 查询指定列
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-FindWhere-1.png" class="img-responsive">
[slide]
* <h6>3.pretty()方法以格式化的方式来显示所有文档。</h6>
* <h6>语法</h6>
<pre><code>db.collection_name.find().pretty()   collection_name 集合的名字
</code></pre>
[slide]
* <h4>实例</h4>
<pre><code> db.worker.find().pretty()
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-pretty-1.png" class="img-responsive">

[slide]
* <h6>4.findOne()方法查询匹配结果的第一条数据</h6>
* <h4>语法</h4>
<pre><code>db.collection_name.findOne()  collection_name 集合的名字
</code></pre>

[slide]
* <h4>实例</h4>
<pre><code>db.worker.findOne()  查询worker下的第一条数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-baoCun-3.png" class="img-responsive">


[slide]
# <h6>查询条件操作符</h6>
* <h6>描述：条件操作符用于比较两个表达式并从mongoDB集合中获取数据。</h6>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-where-1.png" class="img-responsive">

[slide]
* <h6>1.MongoDB (&gt;) 大于操作符 - $gt</h6>
* <h4>语法</h4>
<pre><code>db.collectionName.find({&lt;key&gt;:{$gt:&lt;value&gt;}})<br> collectionName集合名词    key字段    value值
</code></pre>

[slide]
* <h6><实例</h6>
<pre><code>db.worker.find({age:{$gt:30}}) 查询age 大于 30的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-2.png" class="img-responsive">

[slide]
* <h6>2.MongoDB（&gt;=）大于等于操作符 - $gte</h6>
* <h6>语法</h6>
<pre><code>db.collectionName.find({&lt;key&gt;:{$gte:&lt;value&gt;}})<br> collectionName集合名词    key字段    value值
</code></pre>

[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({age: {$gte: 30}}) 查询age 3大于等于30 的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-4.png" class="img-responsive">

[slide]
* <h6>3.MongoDB (&lt;) 小于操作符 - $lt</h6>
* <h4>语法</h4>
<pre><code>db.collectionName.find( {&lt;key&gt;:{$lt:&lt;value&gt;}})<br> collectionName集合名词    key字段    value值
</code></pre>

[slide]
* <h4>实例</h4>
<pre><code>db.worker.find({age: {$lt: 30}}) 查询age 小于30的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-3.png" class="img-responsive">

[slide]
* <h6>4.MongoDB (&lt;=) 小于等于操作符 - $lte</h6>
* <h4>语法</h4>
<pre><code> db.collectionName.find({&lt;key&gt;:{$lte:&lt;value&gt;}}) <br>collectionName集合名词    key字段    value值
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({age: {$lte: 30}}) <br>查询age 小于等于30的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-5.png" class="img-responsive">
[slide]

* <h6>5.MongoDB 使用 (&gt;=) 和 (&lt;=) 查询 - $gte 和 $lte</h6>
* <h4>语法</h4>
<pre><code> db.collectionName.find({&lt;key&gt;:{$gte:&lt;value&gt;},&lt;key&gt;:{$lte:&lt;value&gt;}}) <br>collectionName集合名词    key字段    value值
</code></pre>
[slide]
* <h4>实例</h4>
<pre><code>db.worker.find({age: {$gte: 30, $lte: 50}}) <br>查询age 大于等于 30 并且 age 小于等于 50  的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-6.png" class="img-responsive">
[slide]
* <h6>6.MongoDB 等于（==）</h6>
* <h4>语法</h4>
<pre><code> db.collectionName.find({&lt;key&gt;:&lt;value&gt;,&lt;key&gt;:&lt;value&gt;})<br>   collectionName集合名词    key字段    value值
</code></pre>

[slide]
* <h4>实例</h4>
<pre><code>db.worker.find({"age": 30})`查询age = 30的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-1.png" class="img-responsive">
[slide]
* <h6>7.MongoDB 使用 _id进行查询</h6>
* <h6>语法</h6>
<pre><code>db.collectionName.find({"_id" : ObjectId("value")})  value _id的值
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({"_id" : ObjectId("562af23062d5a57609133974")})<br> 查询_id是 562af23062d5a57609133974 数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-9.png" class="img-responsive">
[slide]
* <h6>8.MongoDB 查询某个结果集的数据的条数</h6>
* <h4>语法</h4>
<pre><code>db.collectionName.find().count()   collectionName集合名称
</code></pre>
[slide]
* <h4>实例</h4>
<pre><code>db.worker.find().count()
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-17.png" class="img-responsive">
[slide]
* <h6>9.MongoDB 查询某个字段的值当中是否包含另一个值</h2>
* <h4>语法</h4>
<pre><code>db.collection.find({key:/value/})  <br> collectionName集合名称 key 字段  value值
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({name:/value/}) 查询name里包含zhang的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-10.png" class="img-responsive">
[slide]
* <h6>10.MongoDB 查询某个字段的值当中是否以另一个值开头</h6>
* <h6>语法</h6>
<pre><code>db.collection.find({key:/^value/})<br>   collectionName集合名称 key 字段  value值
</code></pre>
[slide]
* <h6>实例</h6>
<p>db.worker.find({name:/^zhang/})<br>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-11.png" class="img-responsive"></p>


[slide]
# <h6>查询条件and和or</h6>
* <h6>1.MongoDB AND 条件</h6>
* <h6>MongoDB 的 find() 方法可以传入多个键(key)，每个键(key)以逗号隔开</h6>
* <h6>语法</h6>
<pre><code>db.col.find({key1:value1, key2:value2}).pretty()  
</code></pre>

[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({name:'zhangRenYang',age:30})<br> 查询name是zhangRenYang并且age是30的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-andfind-1.png" class="img-responsive">
[slide]
* <h6>2.MongoDB OR 条件</h6>
* <h6>MongoDB OR 条件语句使用了关键字 $or,语法格式如下：</h6>
* <h6>语法</h6>
<pre><code>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
)
</code></pre>

[slide]
* <h6>实例</h6>
<pre><code>db.worker.find({$or:[{age = 30},{age = 50}]})<br> 查询age = 30 或者 age = 50  的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-8.png" class="img-responsive">
[slide]
* <h6>3.AND 和 OR 联合使用</h6>
* <h4>语法</h4>
<pre><code>db.col.find(
   {
     key1:value1,
     key2:value2,
     $or: [
         {key1: value1},
         {key2:value2}
     ]
   }
)
</code></pre>

[slide]
* <h4>实例</h4>
<pre><code> 查询 name是zhangRenYang 并且 age是30 或者 age是 50 的数据<br>
 db.worker.find({name:'zhangRenYang',$or:[{age:30},{age:50}]})
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/mongodb-andOr-1.png" class="img-responsive">


[slide]
# <h6>MongoDB Limit与Skip方法</h6>
* <h6>1.MongoDB Limit() 方法 读取指定数量的数据记录</h6>
* <h6>语法</h6>
<pre><code>db.collectionName.find().limit(number) <br>   collectionName集合    number读取的条数
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find().limit(3) 查询前3条数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-14.png" class="img-responsive">
[slide]
* <h6>2.MongoDB Skip() 方法 跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。</h6>
* <h6>语法</h6>
<pre><code>db.collectionName.find().skip(number) <br>   collectionName集合    number跳过的条数
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find().skip(3) 查询3条以后的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-15.png" class="img-responsive">
[slide]
* <h6>3.MongoDB Skip()方法和Limit()方法混合使用</h6>
<pre><code>注： 通常用这种方式来实现分页功能
</code></pre>
* <h6>语法</h4>
<pre><code>db.collectionName.find().limit(number).skip(number)  
</code></pre>
[slide]
* <h6>实例</h6>
<pre><code>db.worker.find().limit(3).skip(3) 查询在4-6之间的数据
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-16.png" class="img-responsive">


[slide]
# <h6>排序</h6>
* <h6>MongoDB sort()方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列。</h6>
* <h6>语法</h6>
<pre><code>db.collectionName.find().sort({KEY:1}) <br>或者 db.collectionName.find().sort({KEY:-1})<br>  collectionName集合  key表示字段   
</code></pre>

[slide]
* <h4>实例</h4>
<pre><code>db.worker.find().sort({age:1}) 查询出并升序排序 {age:1}  <br>age表示按那个字段排序 1表示升序
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-12.png" class="img-responsive">
[slide]
<pre><code>db.worker.find().sort({age:-1})<br>  查询出并降序排序  {age:-1} age表示按那个字段排序 -1表示降序
</code></pre>
<img src="http://7xjf2l.com2.z0.glb.qiniucdn.com/3.mongodb-16-13.png" class="img-responsive">
