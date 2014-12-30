### ruby 自学笔记 

**output command:** 

	puts “hello world” 

### 进入交互环境：

irb 

### 语言分类 

分类一: 

静态类型语言: 
	c/c++ java 

动态类型语言: 

	ruby python php javascript/nodejs

分类二: 

强类型语言(strong typing): 

	ruby， java， perl， python

弱类型语言(Weaking typing): 

	php，c, c++


```php
$i  = 1 ;
echo “hello” . $i ; // 会进行自动类型转换 
```

```c
int a = 5; 
float b = a; 
```

c和php会进行自动类型转换, 而ruby却会报错. 

```ruby
i = 1 
puts "value is: " + i 

# TypeError: can't convert Fixnum into String 
# from(irb):2:in `+`
# from(irb):2
```

通常动态语言也是解释行语言(interpreted), 不用事先编译, 通过解释器执行即可. 

综上, Ruby是一门强类型的动态语言, 通过解释器动态执行. 

### Ruby中的类型

**整数Integer**: 

任何整数都市Fixnum对象: 

```ruby
5
-205
999999999
0
```
常用的Fixnum的方法: 

#TODO

**浮点数Float**

中间带有点号的就是Float对象: 

```ruby
54.321
0.01 
-12.321
0.0
```
浮点数的四则运算法则如下: 

```ruby
puts 1.0 + 2.0 	# 3.0
puts 2.0 - 1.0 	# 1.0 
puts 5.0 * 8.0 	# 40.0 
puts 9.0 / 2.0  # 4.5 
```
要注意, 整数的四则运算结果也是整数: 

```ruby
puts 1 + 2 	# 3
puts 2 - 1 	# 1
puts 3 * 4  # 12 
puts 5 / 2 	# 2   
```
常用的Float对象的方法: 

TODO

**字符串String**

使用单引号或者双引号括起来的就是字符串String对象: 

```ruby
puts 'hello world'
puts ''
puts "Good-bye" 
```

字符串可以通过'+'号相加, 但要注意字符串不能直接和数字相加: 

```ruby
puts 'I like ' + 'apple pie' 
puts 'You\'re smart !'

puts '12' + 12 	# <TypeError: can't convert Fixnum into String>
```

更多字符串示例: 

```ruby

var1 = 'stop' 
var2 = 'foobar'
var3 = 'aAbBcC'

puts var1.reverse 	# pots 
puts var2.length 	# 6 
puts var3.upcase 	# AABBCC
puts var3.downcase 	# aabbcc

```

为了更方便字符串的组合, Ruby也支持内插的方式: 

```ruby
verb = 'work'
where = 'office'

puts "I #{verb} at the #{where} " # I work at the office 
```
注意: 使用双引号的字符串才会进行内插处理, 如果换成单引号, 则不处理

String对象常用的API: 

TODO

### Ruby的面向对象 

Ruby是完全的面向对象语言, 它的每样东西都是对象. 包括Fixnum, Float, String都是对象

所有的方法都属于某个对象, 你不会看到全局函数, 比如PHP中的strlen('test'), 在ruby中会写成'test'.length 

```ruby

# UPPER 
puts "upper".upcase 	

# 5
puts -5.abs 

# Fixnum
puts 99.class


# output 5 times [Ruby Rocks!]

5.times do 
	puts "Ruby Rocks!"
end

```

**局部变量** 

局部变量使用小写字母开头, 单词之间使用'_'分隔
如果存取一个尚未初始化的局部变量, 会得到以下错误: 

```ruby
NameError: undefined local variable or method 'qwer' for main 
```

**类型转换Conversions**

上面提到了数字和字符串不能直接相加, 你必须使用to_s(转换成字符串), to_i(转换成整数), to_f(转换成浮点数)来手动转换类型. 

```ruby
var1 = 2
var2 = '5'

puts var1.to_s + var2 # 25 
puts var1 + var2.to_i # 7 

puts 9.to_f / 2 	# 4.5 
```

**常量Constant**

大写开头的为常量 

```ruby
Foo = 1 
Foo = 2 # (irb):3:warning: already initilized constant Foo 

RUBY_PLATFORM 	# => "x86_64-darwin10.7.0"
ENV 			# => {"PATH" => "...", "LC_ALL" => "zh_TW.UTF-8"}
```
**空值nil** 

表示已经声明但为初始化的值: 

```ruby

nil 	# nil 
nil.class 	# NilClass

nil.nil 	# true
42.nil 		# false

nil == nil 	 # true
fasle == nil # false 

```

**ruby注释** 

单行注释 

# this is a comment line 

多行注释比较少见: 

```ruby
=begin 
	This is a comment line
	This is a comment line 
=end

**字符串标识符Symbols** 

Symbols是唯一且不会变动的识别名称, 用冒号开头: 

```rbuy
:this_is_a_symbol
```

为什么不用字符串呢? 这是因为相同名称的Symbol不会再重复创建对象, 所以使用Symbol可以执行的更有效率. 

```ruby
puts "foobar".object_id # output 215131134
puts "foobar".object_id # output 34234234234
puts :foobar.object_id  # output 577768
puts :foobar.object_id  # output 577768
```
object_id方法会返回ruby内部的记忆体配置编号. 两个字符串就算内容相同, 也是不同的对象. 但是Symbol只要内容相同, 就是相同的对象. 这种特性让Symbol的主要用途是Hash的key. 

### 数组Array

使用中括号, 索引从0开始. 数组中的元素不限定为同一类别, 想放什么都可以: 

```ruby
a = [1, "cat", 3.14]

puts a[0] 	# output 1 
puts a.size # output 3 

a[2] = nil 
puts a.inspect # [1, "cat", nil]

a[99] # nil 
```

Array的inspect方法会将对象输出成适合人看的字符串, 类似于js中的toString

如果读取一个没有设置值的数组元素, 预设值时nil. 更多数组方法的示例: 

```ruby

colors = ["red", "blue"]

colors.push("black") 
colors << "white"
puts colors.join(",")  # red, blue, black, white 

colors.pop 
puts colors.last # black 

```

使用each方法遍历数组: 

```ruby
languages = ["ruby", "javascript", "perl"]
languages.each do |lang|
	puts "I love " + lang + "!"
end

# I love ruby 
# I love javascript
# I love perl 
```
完整的Array方法: 

TODO

### Hash/JSON对象

Hash是一种key,value的结构, 虽然你可以使用任何对象当做hash的key, 但通常我们使用Symbol当做key, 例如: 

```ruby

config = { :foo => 123, :bar => 456} 
puts config[:foo] 	# output 123
puts config["nothing"] # nil 

```

在ruby1.9后支持新的语法, 比较简洁: 

```ruby
config = { foo: 123, bar: 456} 

# 等同于

config = { :foo => 123, :bar => 456}

```

使用each方法可以遍历hash: 

```ruby

config = { :foo => 123, :bar => 456}
config.each do |key, value|
	puts "#{key} is #{value}"
end 

# foo is 123
# bar is 456

```

完整的Hash API:

TODO

### 流程控制Flow Control

比较方法: 

```ruby

puts 1 > 2 
puts 1 < 2 
puts 5 >= 5
puts 5 <= 4 
puts 1 ==1 
puts 2 != 1 

puts (2 > 1) && (2 > 3)

```

**控制结构if:** 

```ruby

total = 26000 

if total > 100000 
	puts "large account"
elseif total > 2500 
	puts "medium account"
else 
	puts "small account"
end 

```

如果要执行的if程序只有一行, 可以将if放到行末即可: 

```ruby
puts "greater than ten" if total > 10 
```

**三元运算符**

```ruby

expression ? true_expression : false_expression 

x = 3 
y = (x > 3) ? "foo" : "bar"

```

**控制结构Case**: 

```ruby

case name
	when "John"
		puts "howdy John!"
	when "Ryan"
		puts "Whatz up Ryan"
	else 
		puts "Hi #{name}"
end 
```

**循环while, loop, until, next and bread**

+ while用法: 

```ruby
i = 0 
while (i < 10)
	i += 1 
	next if i %2 == 0  # 跳过双数
end 
```

+ until用法: 

```ruby
i = 0 
i += 1 until i > 10 
puts i 	# 11 
```

+ loop 用法: 

```ruby
i = 0 
loop do 
	i += 1 
	break if i > 10  # 中断循环
end

```

不过, ruby中很少用到while, until, loop. 我们会使用迭代器

** 真或假 ** 

记住, ruby中只有false和nil是假, 其他都是真. 

```ruby

puts "not execute" if nil
puts "not execute" if false

puts "execute" if true # 輸出 execute
puts "execute" if “” # 輸出 execute (和JavaScript不同)
puts "execute" if 0 # 輸出 execute (和C不同)
puts "execute" if 1 # 輸出 execute
puts "execute" if "foo" # 輸出 execute
puts "execute" if Array.new # 輸出 execute

```

### 正则表达式 Regular Expression

类似Perl类似的语法, 使用=~: 

```ruby
# 获取手机号
phone = "123-456-789"
if phone =~ /(\d{3})-(\d{3})-(\d{3})/
	ext = $1 
	city = $2
	num = $3  
end 
```

### 定义方法Methods

使用def开头, end结尾来定义一个方法: 

```ruby
def say_hello(name)
	result = "Hi, " + name 
	return result 
end 

puts say_hello('ihover')
# output Hi, ihower 
```

方法中的return是可以省略的, Ruby就会返回最后一行运算的值. 上述方法可以定义成: 

```ruby
def say_hello(name)
	"Hi, " + name 
end 
```
调用方法时, 括号也是可以省略的, 例如: 

```ruby
	say_hello 'ihover'
```

不过, 除了一些方法惯例不加之外(例如puts和Rails中的redirect_to, render), 绝大部分情况要加上括号. 

我们也可以给方法参数预设值: 

```ruby

def say_hello(name = "nobody")
	result = "Hi, " + name
	return result
end 

puts say_hello 	 # output Hi, nobody 

```
不用传递参数的方法可以不用带上"()"来调用. 

** ?与!的惯例 ** 

方法名称可以用?或!结尾, 前者表示会返回Boolean值, 后者暗示会有某种副作用(side-effect), 例如: 

```ruby

array = [2, 1, 3]

array.empty? 	# false 
array.sort 		# [1, 2, 3]

array.inspect 	# [2, 1, 3]

array.sort! 	# [1, 2, 3]
array.inspect 	# [1, 2, 3]

```

### ruby面向对象

ruby中的class是以大写字母开头, 其实也是一种常数, 使用new方法可以创建对象.

之前所学的字符串, 数组和Hash, 可以通过如下方式建立: 

```ruby

color_string = String.new
color_string = "" 	# 等同

color_array = Array.new 
color_array = []  	# 等同

color_hash = Hash.new
color_hash = {} 	# 等同

time = Time.new 	# 内建的时间类型
puts time 

```

如何自定义类型: 

```ruby

class Person 

	def initialize(name)
		@name = name # 成员变量
	end 

	def say(word)
		puts "${word}, #{name}"
	end
end 

p1 = Person.new("ihower")
p2 = Person.new("ihover")

p1.say("Hello")		# Hello, ihower 
p2.say("Hello")		# Hello, ihover 

```

在双引号字符串中使用#{var}来作字符串嵌入, 比"+"相加更有效率. 

除了对象方法与对象变量, Ruby也有属于类方法和类变量: 

```ruby

class Person 
	
	@@name = "ihower" 	# 类变量

	def self.say 
		puts @@name 
	end 

end 

Person.say 	# ihower 

```

**对象封装**

所有的对象变量(@开头), 类变量(@@开头), 都是封装在类内部的, 类外的代码是无法存取的: 

```ruby

class Person 

	def initalize(name)
		@name = name 
	end 

end 

p = Person.new('ihower')
p.name 	# 出现NoMethodError错误
p.name = 'peny' # 出现NoMethodError错误

```
为了可以存取到@name, 我们必须定义方法: 

```ruby

class Person 

	def initialize(name)
		@name = name 
	end 

	def name 
		@name 
	end 

	def name=(name)
		@name = name 
	end 
end 

p = Person.new('ihower')
=> #<Person:ox0007add @name="ihower">

p.name # 'ihower'
p.name = "peny" # peny

```

**类class定义范围内也可以执行程序**

与其他语言不同的是, ruby的class内野可以执行程序, 例如: 

```ruby

class Demo 
	puts "foobar"
end 

```

当你载入这个class时, 就会执行puts "foobar" 输入foobar. 
这个特性主要用来做Meta-programming. 例如, 上述定义对象变量的存取方法实在太常见了, 因此ruby提供了attr_accessor, attr_writer, attr_reader类方法可以直接定义这些方法. 所以, 上述程序可以改成: 

```ruby

class Person 

	attr_accessor :name 

	def initialize(name)
		@name = name 
	end

end 

p = Person.new('ihower')
p.name # ihower 
p.name = "peny" # peny 


```

**方法封装**

类中的方法默认的都是public的, 如果要声明private或者protected的方法, 主要定义在private和protected关键字后即可: 

```ruby

class MyClass

	def public_method 
	end 

	private 

	def private_method_1
	end 

	def private_method_2
	end 

	protected

	def protected_method 
	end 

end 

```

ruby中的private和protected和其他语言不同, 都是可以再整个继承体系内调用, 两者的区别在于private只有在对象内部才能调用, 调用者只能是对象本身, 也就是self. 而protected方法除了可以在本身内部调用以外, 还可以被子类对象, 或是另一个相同类别的对象调用. 

在面向对象的术语中, object.call_method 的意思时object收到执行call_method的指令, 也就是object是call_method方法的调用者,一次, 你甚至可以改写成object.__send__(:call_method)

### Class继承

Ruby使用小于号"<"符号代表类继承: 

```ruby

class Pet

	attr_accessor :name, :age

	def say(word)
		puts "say: #{word}"
	end 
end 

class Cat < Pet

	def say(word)
		puts "Meow~"
		super
	end 

end 

class Dog < Pet 

	def say(word, person)
		puts "Bark at #{person}"
		super(word)
	end

end 

Cat.new.say("Hi")
Dog.new.say("Hi","ihower")

# Meow~
# Say: Hi
# Bark at ihower! 
# Say: Hi

```
这个范例中, Cat和Dog子类覆盖了Pet的say方法, 其中super是用来呼叫被覆盖掉的Pet say方法. 另外, 没有括号的super和有括号的super()是又差异的, 前者ruby会自动将所有参数传递进去, 后者则是自己指定参数. 

此例中, 如果Dog say里只写super, 则会产生wrong number of arguments的错, 这是因为ruby会传say("Hi", "ihower")给Pet say而发生错误. 

### Module

Module是ruby的一个非常好用的功能, 它跟Class非常相识, 你可以在里面定义方法. 只是你不能用new来创建.

Module的第一个用途是用来做Namespace存放一些工具方法: 

```ruby

module MyUtil

	def self.foobar
		puts "foobar"
	end 
end

MyUtil.foobar # foobar 
```
另一个更重要的功能是Mixins, 可以讲一个Module混入class中, 这样这个类就会拥有此Module的方法. 例如:

debug.rb: 

```ruby

module Debug

	def who_am_i?
		puts "#{self.class_name}: #{self.inspect}"
	end
end

```

foobar.rb

```ruby

require "./debug"

class Foo
	inclue Debug 	# 这个动作叫做Mixin
end 

class Bar
	include Debug 
end 

f = Foo.new
b = Bar.new
f.who_am_i?  # Foo: #<Foo: 0x00000000>
b.who_am_i?  # Bar: #<Bar: 0x000000>	

```
Ruby使用Module来解决多重继承的问题, 不同类之间但是拥有相同的方法, 就可以改放在Module里面, 然后include它既可. 

### 迭代器Iterator

不同于while循环用法, Ruby习惯使用迭代器(Iterator)来访问循环. 例如each是一个数组的方法, 它会循环访问其中的元素, do ... end 是each方法的参数, 称为匿名方法(code block): 

```ruby

languages = ['Ruby', 'Javascript', 'Perl']
languages.each do |lang|
	puts "I love #{lang}"
end 

# I love Ruby
# I love Javascript
# I love Perl 

```
其中两个'|'中间的lang被称作Block variable区块变量, 每次迭代都被设置为不同元素. 其他迭代器范例: 

```ruby
# 反复3次

3.tims do |time|
	puts "Good Job!"
end 

# Good Job
# Good Job
# Good Job

# 从一到九
1.upto(9) do |x|
	puts x
end 

# 多一个索引区块变量
languages = ['Ruby', 'Javascript', 'Perl']
languages.each_with_index do |lang, i|
	puts "#{i}, I love #{lang}"
end 

# 0, I love Ruby
# 1, I love Javascript
# 2, I love Perl 

```

Code block的行驶除了使用do...end, 也可以改用大括号, 通常单行会使用大括号, 多行会使用do...end的形式: 

```ruby
3.times { puts "Hello"}
```

**其他迭代方法范例**

```ruby

# 迭代且造出另一个数组
a = ["a", "b", "c", "d"]
b = a.map {|x| x + "!"}

puts a.inspect  # ["a!", "b!", "c!"]

# 找出符合条件的值
b = [1, 2, 3].find_all {|x| x %2 == 0 }
b.inspect 	# [2]

# 迭代并根据条件删除
a = [51, 101, 256]
a.delete_if {|x| x >= 100}
# [51]

# 定制化配需
[2, 1, 3].sort {|a, b| b <=> a}
# [3, 2, 1]

# 计算总和
(5..10).inject {|sum, n| sum+n}
# 45 

# 找出最长字符串
longest = ["cat", "sheep", "bear"].inject do |memo, word|
	(memo.length > word.length) ? memo : word
end 
# "sheep"

```

"<=>"是比较运算子, 当两个数字相等时返回0, 第一个数字较大时返回1, 反之返回-1 

**仅执行一次调用**

除了迭代, Code block只会执行一次的特性也很有用, 例如用来开启文件, 往常我们在文件处理完毕之后, 会使用close方法关闭: 

```ruby
file = File.new('testfile', "r")
...
file.close 

```
改为Code block语法之后, Ruby就会在Code block结束后自动关闭: 

```ruby
File.open("testfile", "r") do |file|
	# ...
end 

# file会自动关闭
```

Code block的这个特性不知让你少打close方法, 更可以避免你忘记关闭file流, 也有视觉上缩排的好处. 

### Yield

在方法中使用yield可以执行Code block参数: 

```ruby
# 定义方法
def call_block
	puts "Start"
	yield 
	yield 
	puts "End"
end 

call_block { puts "Blocks are cool !"}

# "Start"
# "Blocks are cool!"
# "Blocks are cool!"
# "End"
```

**带有参数的Code block**

```ruby
def call_back
	yield(1)
	yield(2)
	yield(3)
end 

call_block {|i|
	puts "#{i}: Blocks are cool!"
}

# "1: Blocks are cool!"
# "2: Blocks are cool!"
# "3: Blocks are cool!"

```

**Proc object**

可以讲Code block明确转成一个变量: 

```ruby
def call_block(&block)
	block.call(1)
	block.call(2)
	block.call(3)
end 

call_block {|i| puts "#{i}: Blocks are cool!"}

# "1: Blocks are cool!"
# "2: Blocks are cool!"
# "3: Blocks are cool!"

# 或是先构造出proc object 
proc_1 = Proc.new { |i| puts "#{i}: Blocks are cool! "}
proc_2 = Proc.new { |i| puts "#{i}: Blocks are cool!"}

call_block(&proc_1)
call_block(&proc_2)


# "1: Blocks are cool!"
# "2: Blocks are cool!"
# "3: Blocks are cool!"
```

**传递不定参数**

```ruby
def my_sum(*val)
	val.inject { |sum, v| sum + v}
end 

puts my_sum(1, 2, 3, 4) # [1, 2, 3, 4]
```
其中my_sum方法中val是一个包含所有参数的数组

**参数尾巴的Hash可以省略{}**

```ruby
def my_print(a, b, options)
	puts a 
	puts b 	
	puts options[:x]
	puts options[:y]
	puts options[:z]
end 

my_print("A", "B", {:x => 123, :z => 456})
my_print("A", "B", :x => 123, :z => 456)

# A
# B
# 123
# nil
# 456

```

**异常处理**

使用rescue可以将异常救回来: 

```ruby
begin 
	puts 10/0 # 这回爆出ZeroDivisionError
rescue => e 
	puts e.class # 如果抛出异常会执行这一行
ensure
	# 无论有没有抛出异常, ensure这一行都会执行
end 

```

**使用raise可以手动抛出异常**

```ruby
raise "Not works!"
# throw Runtime Exception 

# 自定义异常
class MyException < RuntimeError
	# ... 
end 

raise MyException 

```

### Metaprogramming 用程序写程序

Metaprogramming是一个进阶技巧, 这里示范使用define_method方法可以动态定义方法: 

```ruby
class Dragon

	define_method(:foo) { puts "bar"}

	['a', 'bc','c','d','e','f'].each do |x| 
		define_method(x) { puts x}
	end 
end 

dragon = Dragon.new 
dragon.foo  	# bar
dragon.a 		# a
dragon.b 		# b

``` 

### introspection 反射机制

Ruby拥有许多反射方法, 可以动态知道对象的信息: 

```ruby

# 返回对象拥有的方法
Object.methods 
# => ["send", "name", "class_eval", "object_id", "new", "singleton_methods",...]

# 这个对象有这个方法吗? 
Object.response_to ? :name 
# true

```

### 其他常见惯例

```ruby
result ||= a 
```
如果result是nil或false的话, 将a赋值给reuslt, 如果不是的话, 什么都不做. 以上代码等同于: 

```ruby
result || (result = a)
```

### Ruby 应用

+ Sinatra: 轻量级的Web框架
+ 网页设计: 

	+ Sass: CSS Pre-Processor
	+ Less: CSS Pre-Processor
	+ Compass: CSS设计框架
	+ Middleman: 静态网站产生工具
	+ Jekyll: 静态网站和Blog产生工具

+ 自动化测试: 

	+ Cucumber: BDD测试框架
	+ Watir: 自动化浏览器测试工具

+ DevOps: 

	+ Chef: 服务器部署工具
	+ Puppet: 服务器部署工具
	+ Vagrant: 虚拟机工具

+ iOS/Mac
	
	+ CocoaPods: Object-C的套件管理工具
	+ RubyMotion: Object-C的ruby

+ Redmine: 专业任务管理平台


			

















