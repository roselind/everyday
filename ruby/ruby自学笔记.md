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












