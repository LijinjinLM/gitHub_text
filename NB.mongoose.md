[slide]
# <h6>一、简介</h6>
* Mongoose是MongoDB的一个对象模型工具，是基于node-mongodb-native开发的MongoDB nodejs驱动，可以在异步的环境下执行。同时它也是针对MongoDB操作的一个对象模型库，封装了MongoDB对文档的的一些增删改查等常用方法，让NodeJS操作Mongodb数据库变得更加灵活简单。
[slide]
* <h6>2.Mongoose能做什么？</h6>
* <h6>Mongoose，因为封装了对MongoDB对文档操作的常用处理方法，让NodeJS操作Mongodb数据库变得更加容易。</h6>
[slide]
* <h6>二、安装使用mongoose：</h6>
    <pre><code>npm install mongoose
</code></pre>
* <p>引用mongoose：</p>
    <pre><code>var mongoose = require("mongoose");
</code></pre>

[slide]
* <p>使用"mongoose"连接数据库：</p>
    <pre><code>var db = mongoose.connect<br>("mongodb://user:pass@localhost:port/database");
</code></pre>
[slide]
    <p>执行下面代码检查默认数据库test，是否可以正常连接成功?</p>
    <pre><code>var mongoose = require("mongoose");
var db = mongoose.connect("mongodb://127.0.0.1:27017/zking");
db.connection.on("error", function (error) {
    console.log("数据库连接失败：" + error);
});
db.connection.on("open", function () {
    console.log("数据库连接成功");
});
</code></pre>
[slide]
* <h6>三、集合</h6>
* MongoDB —— 是一个对象数据库，没有表、行等概念，也没有固定的模式和结构，所有的数据以Document(以下简称文档)的形式存储(Document，就是一个关联数组式的对象，它的内部由属性组成，一个属性对应的值可能是一个数、字符串、日期、数组，甚至是一个嵌套的文档。)，后面我们会学习如何创建文档并插入内容。

[slide]
* <p>在MongoDB中，多个Document可以组成Collection(以下简称集合)，多个集合又可以组成数据库。</p>
* <p>我们想要操作MongoDB数据，那就得先要具备上面所说的包含数据的“文档”，文档又是什么意思呢，请看如下介绍。</p>
[slide]
* <p>文档 —— 是MongoDB的核心概念，是键值对的一个有序集，在JavaScript里文档被表示成对象。同时它也是MongoDB中数据的基本单元，非常类似于关系型数据库管理系统中的行，但更具表现力。</p>
[slide]
* <p>集合 —— 由一组文档组成，如果将MongoDB中的一个文档比喻成关系型数据库中的一行，那么一个集合就相当于一张表。</p>
* <p>如果我们要通过Mongoose去创建一个“集合”并对其进行增删改查，该怎么实现呢，到这里我们就要先了解Schema(数据属性模型)、Model、Entity了。</p>
[slide]
* <h6>四、Schema简述</h6>
* <p>Schema —— 一种以文件形式存储的数据库模型骨架，无法直接通往数据库端，也就是说它不具备对数据库的操作能力，仅仅只是数据库模型在程序片段中的一种表现，可以说是数据属性模型(传统意义的表结构)，又或着是“集合”的模型骨架。</p>
[slide]
* <p>那如何去定义一个Schema呢，请看示例：</p>
<pre><code>var PersonSchema = new mongoose.Schema({
    name : { type:String },
    age  : { type:Number, default:0 },
    time : { type:Date, default:Date.now },
    email: { type:String,default:''}
});
</code></pre>
[slide]
* <p>基本属性类型有：字符串、日期型、数值型、布尔型(Boolean)、null、数组、内嵌文档等。</p>
* <h6>五、Model简述</h6>
* <p>Model —— 由Schema构造生成的模型，除了Schema定义的数据库骨架以外，还具有数据库操作的行为，类似于管理数据库属性、行为的类。</p>
[slide]
* <p>如何通过Schema来创建Model呢，如下示例：</p>
<pre><code>var db = mongoose.connect("mongodb://127.0.0.1:27017/zking");
//创建Model
var PersonModel = db.model("person", PersonSchema);
</code></pre>
[slide]
* <p>person：数据库中的集合名称,当我们对其添加数据时如果person已经存在，则会保存到其目录下，如果未存在，则会创建person集合，然后在保存数据。</p>
* <p>拥有了Model，我们也就拥有了操作数据库的能力</p>
[slide]
* <p>如果你想对某个集合有所作为，那就交给Model模型来处理吧，创建一个Model模型，我们需要指定：</p>
<ul>
  <li>1.集合名称，</li>
  <li>2.集合的Schema结构对象，满足这两个条件，我们就可以操作数据库啦。</li>
</ul>
[slide]
* <h6>六、Entity简述</h6>
* <p>Entity —— 由Model创建的实体，使用save方法保存数据，Model和Entity都有能影响数据库的操作，但Model比Entity更具操作性。</p>
* <p>使用Model创建Entity，如下示例：</p>
<pre><code>var personEntity = new PersonModel({
    name : "tom",
    age  : 6,
    email: "zking@qq.com"
});
console.log(personEntity.name); // tom
console.log(personEntity.age); // 6
</code></pre>
[slide]
* <p>创建成功之后，Schema的属性就变成了Model和Entity的公共属性了。</p>
[slide]
* <h6>七、创建基础集合数据</h6>
* 先定义数据库和集合，数据库叫zking,集合叫person
[slide]
<pre><code>var mongoose = require("mongoose");
var mongoose = require("mongoose");
var db = mongoose.connect("mongodb://127.0.0.1:27017/zking");
db.connection.on("error", function (error) {
    console.log("数据库连接失败：" + error);
});
db.connection.on("open", function () {
    console.log("数据库连接成功");
});
</code></pre>
[slide]
<pre><code>
var mongoose = require("mongoose");
var PersonSchema = new mongoose.Schema({
    name : { type:String },
    age  : { type:Number, default:0 },
    time : { type:Date, default:Date.now },
    email: { type:String,default:''}
});
var db = mongoose.connect("mongodb://127.0.0.1:27017/zking");
var PersonModel = db.model("person", PersonSchema);
var personEntity = new PersonModel({
    name : "tom",
    age  : 6,
    email: "zking@qq.com"
});
console.log(personEntity.name); // tom
console.log(personEntity.age); // 6
</code></pre>
[slide]
<pre><code>
personEntity.save(function(error,doc){
    if(error){
        console.log("error :" + error);
    }else{
        console.log(doc);
    }
});
</code></pre>
[slide]
* <h6>八、小结：</h6>
<ol>
  <li>Schema：数据库集合的模型骨架，或者是数据属性模型传统意义的表结构。</li>
  <li>Model ：通过Schema构造而成，除了具有Schema定义的数据库骨架以外，还可以具体的操作数据库。</li>
  <li>Entity：通过Model创建的实体，它也可以操作数据库。</li>
</ol>


[slide]
# <h6>查询</h6>
* <p>上节课程里集合已经创建成功，我们就先来进行第一步操作 —— 查询。</p>
* <p>查询分很多种类型，如条件查询，过滤查询等等，今天我们只学习最基本的find查询，在后面的学习中，我们会专门针对查询做详细的介绍，好，我们就先来学习使用find查询。</p>

[slide]
# <h6>1.find查询： obj.find(查询条件,callback);</h6>
<pre><code>Model.find({},function(error,docs){
   //若没有向find传递参数，默认的是显示所有文档
});

Model.find({ "age": 6 }, function (error, docs) {
  if(error){
    console.log("error :" + error);
  }else{
    console.log(docs); //docs: age为6的所有文档
  }
}); </code>
</pre>

[slide]

# <h6>Model保存方法</h6>

* <p>Model提供了一个create方法来对数据进行保存。下面我们来看一下示例：</p>

<ol>
	<li>Model.create(文档数据, callback))
	<pre><code>PersonModel.create({ name:"zking", age:7}, function(error,doc){
    if(error) {
        console.log(error);
    } else {
        console.log(doc);
    }
});</code>
</pre>
	</li>
</ol>

[slide]
# <h6>entity保存方法</h6>
* <h6>刚刚学习了model的create方法，那接下来就开始学习基于entity的保存方法吧。如下示例：</h6>
<ol>
	<li>Entity.save(文档数据, callback))</li>
</ol>
<pre><code>
var PersonEntity = new PersonModel({name:"zking",age: 9});
PersonEntity.save(function(error,doc) {
if(error) {
console.log(error);
} else {
console.log(doc);
}
});
</code></pre>
[slide]
* <p>model调用的是create方法，entity调用的是save方法.</p>
[slide]
# <h6>数据更新</h6>
* 学习了数据的保存，接下来我们就开始学习对数据的更新
* 1.示例：Model.update(查询条件,更新对象,callback);
<pre><code>var conditions = {name : 'zking'};
var update = {$set : { age : 100 }};
PersonModel.update(conditions, update, function(error){
    if(error) {
        console.log(error);
    } else {
        console.log('Update success!');
    }
});
</code>
</pre>
[slide]
<p>更新后find一下，此时数据已经修改成功了！请注意如果匹配到多条记录，默认只更新一条，如果要更新匹配到的所有记录的话需要加一个参数&nbsp;{multi:true}</p>

<pre><code>PersonModel.update(conditions, update,{multi:true},function(error){
    if(error) {
        console.log(error);
    } else {
        console.log('Update success!');
    }
});</code>
</pre>

[slide]
# <h6>删除数据</h6>
* 有了数据的保存、更新，就差删除了
* 1.示例：Model.remove(查询条件,callback);
<pre><code>var conditions = { name: 'zking' };
PersonModel.remove(conditions, function(error){
    if(error) {
        console.log(error);
    } else {
        console.log('Delete success!');
    }
});
</code>
</pre>
[slide]
* 和update类似吧，有了remove方法我们就可以进行删除操作了.

[slide]
<h6>小结</h6>

<ol>
	<li>查询：find查询返回符合条件一个、多个或者空数组文档结果。</li>
	<li>保存：model调用create方法，entity调用的save方法。</li>
	<li>更新：obj.update(查询条件,更新对象,callback)，根据条件更新相关数据。</li>
	<li>删除：obj.remove(查询条件,callback)，根据条件删除相关数据。</li>
</ol>
[slide]
* <p>查询就是返回一个集合中的文档的子集，Mongoose 模型提供了find、findOne、和findById方法用于文档查询。</p>
[slide]
* <p>我们这里先添加一些测试数据。</p>
<pre><code>    PersonModel.create([
                      { name:"zking1", age:1 },
                      { name:"zking2", age:2 },
                      { name:"zking3", age:3 },
                      { name:"zking4", age:4 },
                      { name:"zking5", age:5 },
                      { name:"zking6", age:6},
                      { name:"zking7", age:7 },
                      { name:"zking8", age:8 },
                      { name:"zking9", age:9},
                     ], function(error,docs) {
        if(error) {
            console.log(error);
        } else {
            console.log('save ok');
        }});</code></pre>
[slide]
* <h6>属性过滤 find(Conditions,field,callback);</h6>
* <p>field省略或为Null，则返回所有属性。</p>
<pre><code>//返回只包含name、age两个键的所有记录
Model.find({},{name:1, age:1, _id:0}，function(err,docs){
   //docs 查询结果集
})
</code></pre>
[slide]
* <p>说明：我们只需要把显示的属性设置为大于零的数就可以，当然1是最好理解的，_id是默认返回，如果不要显示加上("_id":0)，但是，对其他不需要显示的属性且不是_id，<br>如果设置为0的话将会抛异常或查询无果。</p>
[slide]
* <h6>findOne(查询单条)</h6>
* <p>与find相同，但只返回单个文档，也就说当查询到即一个符合条件的数据时，将停止继续查询，并返回查询结果。</p>
* <p>1.单条数据 findOne(Conditions,callback);</p>
<pre><code>TestModel.findOne({ age: 6}, function (err, doc){
   // 查询符合age等于6的第一条数据
   // doc是查询结果
});
</code></pre>
* <p>findOne方法，只返回第一个符合条件的文档数据。</p>
[slide]
* <h6>findById(按ID单条数据)</h6>
* <p>与findOne相同，但它只接收文档的_id作为参数，返回单个文档。</p>
* <p>1.按ID单条数据 findById(_id, callback);</p>
<pre><code>PersonModel.findById(person._id, function (err, doc){
 //doc 查询结果文档
});
</code></pre>
[slide]
<h6>小节</h1>
<ol>
  <li>find过滤查询 ：find查询时我们可以过滤返回结果所显示的属性个数。</li>
  <li>findOne查询 ：只返回符合条件的首条文档数据。</li>
  <li>findById查询：根据文档_id来查询文档。</li>
</ol>

[slide]
# <h6>$gt、$lt(大于、小于)</h1>
* <p>查询时我们经常会碰到要根据某些字段进行条件筛选查询，比如说Number类型，怎么办呢，我们就可以使用$gt(&gt;)、$lt(&lt;)、$lte(&lt;=)、$gte(&gt;=)操作符进行排除性的查询，如下示例：</p>
[slide]
<pre><code>Model.find({"age":{"$gt":6}},function(error,docs){
   //查询所有nage大于6的数据
});
Model.find({"age":{"$lt":6}},function(error,docs){
   //查询所有nage小于6的数据
});
Model.find({"age":{"$gt":6,"$lt":9}},function(error,docs){
   //查询所有nage大于6小于9的数据
});
</code></pre>
[slide]
* <h6>$ne(不等于)</h6>
* <p>$ne(!=)操作符的含义相当于不等于、不包含，查询时我们可通过它进行条件判定，具体使用方法如下：</p>
<pre><code>Model.find({ age:{ $ne:6}},function(error,docs){
    //查询age不等于24的所有数据
});
Model.find({name:{$ne:"zking"},age:{$gte:6}},function(error,docs){
  //查询name不等于zking、age&gt;=6的所有数据
});
</code></pre>
<p>$ne可以匹配单个值，也可以匹配不同类型的值。 </p>
[slide]
* <h6>$in(包含)</h6>
* <p>和$ne操作符相反，$in相当于包含、等于，查询时查找包含于指定字段条件的数据。具体使用方法如下：</p>
<pre><code>Model.find({ age:{ $in: 6}},function(error,docs){
   //查询age等于6的所有数据
});
del.find({ age:{$in:[6,7]}},function(error,docs){
  //可以把多个值组织成一个数组
});
</code></pre>
<p>$in和$ne除了条件判定不同，用法很相似！</p>
[slide]
* <h6>$or(或者)</h6>
* <p>$or操作符，可以查询多个键值的任意给定值，只要满足其中一个就可返回，用于存在多个条件判定的情况下使用，如下示例：</p>
<pre><code>Model.find({"$or":[{"name":"zking"},{"age":6}]},function(error,docs){
  //查询name为zking或age为6的全部文档
});
</code></pre>
[slide]
* <h6>$exists(是否存在)</h6>
* <p>$exists操作符，可用于判断某些关键字段是否存在来进行条件查询。如下示例：</p>
<pre><code>Model.find({name: {$exists: true}},function(error,docs){
  //查询所有存在name属性的文档
});
Model.find({email: {$exists: false}},function(error,docs){
  //查询所有不存在email属性的文档
});
</code></pre>



[slide]
* <p>数据库使用游标返回find的执行结果。客户端对游标的实现通常能够对最终结果进行有效的控制。可以限制结果的数量，略过部分结果，根据任意键按任意顺序的组合对结果进行各种排序，或者是执行其他操作。</p>
* <p>最常用的查询选项就是限制返回结果的数量(limit函数)、忽略一点数量的结果(skip函数)以及排序(sort函数)。所有这些选项一点要在查询被发送到服务器之前指定。</p>
[slide]
* <h6>limit函数的基本用法</h6>
* <p>在查询操作中，有时数据量会很大，这时我们就需要对返回结果的数量进行限制，那么我们就可以使用limit函数，通过它来限制结果数量。</p>
* <p>1.限制数量：find(Conditions,fields,options,callback);</p>
[slide]
<pre><code>Model.find({},null,{limit:20},function(err,docs){
    console.log(docs);
});
</code></pre>
<p>如果匹配的结果不到20个，则返回匹配数量的结果，也就是说limit函数指定的是上限而非下限。</p>
[slide]
* <h6>skip函数的基本用法</h6>
* <p>skip函数和limit类似，都是对返回结果数量进行操作，不同的是skip函数的功能是略过指定数量的匹配结果，返回余下的查询结果。如下示例：</p>
[slide]
* <p>1.跳过数量：find(Conditions,fields,options,callback);</p>
<pre><code>Model.find({},null,{skip:4},function(err,docs){
    console.log(docs);
});
</code></pre>
<p>如果查询结果数量中少于4个的话，则不会返回任何结果。</p>
[slide]
* <h6>sort函数的基本用法</h6>
* <p>sort函数可以将查询结果数据进行排序操作，该函数的参数是一个或多个键/值对，键代表要排序的键名，值代表排序的方向，1是升序，-1是降序。</p>
[slide]
* <p>1.结果排序：find(Conditions,fields,options,callback);</p>
<pre><code>Model.find({},null,{sort:{age:-1}},function(err,docs){
  //查询所有数据，并按照age降序顺序返回数据docs
});
</code></pre>
<p>sort函数可根据用户自定义条件有选择性的来进行排序显示数据结果。</p>
[slide]
* <h6>小结</h6>
<ol>
  <li>limit函数：限制返回结果的数量。</li>
  <li>skip函数：略过指定的返回结果数量。</li>
  <li>sort函数：对返回结果进行有效排序。</li>
</ol>


[slide]
* <h6>ObjectId简述</h6>
* <p>存储在mongodb集合中的每个文档（document）都有一个默认的主键_id，这个主键名称是固定的，它可以是mongodb支持的任何数据类型，默认是ObjectId。该类型的值由系统自己生成，从某种意义上几乎不会重复</p>
[slide]
* <p>MySQL等关系型数据库的主键都是自增的。但在分布式环境下，这种方法就不可行了，会产生冲突。为此，MongoDB采用了一个称之为ObjectId的类型来做主键。ObjectId是一个12字节的 BSON 类型字符串。按照字节顺序，依次代表：</p>
[slide]
<ul>
  <li>4字节：UNIX时间戳</li>
  <li>3字节：表示运行MongoDB的机器</li>
  <li>2字节：表示生成此_id的进程</li>
  <li>3字节：由一个随机数开始的计数器生成的值
    <p>var mongoose = require('mongoose');</p>
    <p>var personSchema = new mongoose.Schema({}); //默认_id:ObjectId类型</p>
  </li>
</ul>
* <p>每一个文档都有一个特殊的键“_id”，这个键在文档所属的集合中是唯一的。</p>
[slide]
* <h6>Schema添加属性值</h6>
* <p>前面我们已经讲述了如何定义一个Schema并赋予某些属性值,那能不能先定义后添加属性呢，答案是可以的，如下所示：</p>
<pre><code>var mongoose = require('mongoose');
var PersonSchema = new mongoose.Schema;
PersonSchema.add({ name: 'String', email: 'String', age: 'Number' });
</code></pre>
[slide]
* <h6>实例方法</h6>
* 有的时候，我们创造的Schema不仅要为后面的Model和Entity提供公共的属性，还要提供公共的方法.那怎么在Schema下创建一个实例方法呢，请看示例：
<pre><code>var mongoose = require('mongoose');
var personSchema = new mongoose.Schema({name : String});
personSchema.method('greet', function () {
  console.log('how are you');
})
var Person = mongoose.model('person', personSchema);
var person = new Person();
person.greet(); //how are you
</code></pre>
[slide]
* <h6>Schema静态方法</h6>
* <p>接下来将讲述怎么为Schema创建静态方法：</p>
<pre><code>var mongoose = require("mongoose");
var db = mongoose.connect("mongodb://127.0.0.1:27017/zking");
var PersonSchema = new mongoose.Schema({
    name : { type:String },
    age  : { type:Number, default:0 },
});
PersonSchema.static('findByName', function (name, callback) {
    return this.find({ name: name }, callback);
});
var PersonModel = db.model("person", PersonSchema );
PersonModel.findByName('zking', function (err, docs) {
 //docs所有名字叫zking的文档结果集
});
</code></pre>
