ruby自学笔记

ruby 打印语句: 

* print(str), 打印日志, 不加换行符
* puts,打印日志, 默认加上换行符
* p, 打印对象
* pp, pretty print, 

从命令行中输入数据: 

```ruby

# 命令行参数对象ARGV
puts "first agrm: #{ARGV[0]}"
puts "second arg: #{ARGV[1]}"
puts "third arg: #{ARGV[2]}"

```

### 对象, 变量和常量

**变量**

- 局部变量
以英文字母或者'_'开头
- 全局变量
以$开头
- 实例变量
以@开头
- 类变量
以@@开头

除了以上4中类型外, 还有一种称为伪变量(pseudo variable)的特殊变量 . nil, false, true, self都是伪变量. 其实还有一种预定义变量(Pre-defined variable). 

2个同名的局部变量代表不同的变量. 而2个同名的全局变量代表着相同的一个变量 

**常量** 

常量以大写字母开头. 一般全部大写. 比如: ruby运行版本(RUBY_VERSION), 运行平台(RUBY_PLATFORM), 命令行参数(ARGV)

**多重赋值**

```ruby
a, b, c = 1, 2, 3 
a, b, c, d = 1, 2 # c,d 为nil
a, b, c = 1, 2, 3, 4 # 忽略4 

# 变量前加*, 表示ruby会将未分配的值封装为数组赋值给该变量 
a, b, *c = 1, 2, 3, 4, 5  # c = [3, 4, 5]
a, *b, c = 1, 2, 3, 4, 5 # b = [2,3,4]
```

**交换变量的值**

```ruby
a, b = 1, 0
a, b = b, a 
p [a, b] # => [1, 0]

```
**用数组赋值**

```ruby
arr = [1, 2]
a, b = arr
p [a, b] # => [1, 2]

# 只获取数组的开头元素
arr = [1,2]
a, = arr 
p a # => 1 
```

**获取嵌套数组的元素**

```ruby
arr = [1, [2,3], 4]
a, b, c = arr
p a # 1
p b # [2, 3]
p c # 4 

```

**进一步取出嵌套数组的元素**

```ruby
arr = [1, [2, 3], 4]
a, [b1, b2], c = arr
p a # => 1
p b1 # => 2
p b2 # => 3
p c  # => 4
```

**总结: 变量的命令方法**

- 以变量名开头来决定变量的种类, 这是ruby中对变量命令的唯一要坚决遵守的规则. 
- 不要过多使用省略的名称
- 对于多个单词组合的变量名, 使用'_'隔开各个单词, 或者单词以大写字母开头. ruby中的变量名使用前者, 类名和模块名使用后者. 

### 条件判断

除了nil, false为假, 其他都为真. 

```ruby
if con then
	# condition
elseif con then
	# condition 
else
	# condition 
end 
```
unless语句的用法和if相反.

case...when和js中的switch...case

```ruby
case err
when err == 'error' then
	puts 'error'
when err == 'ok' then
	puts 'ok'	 
else 
	puts 'unknow'
end
```
when中默认已经带上了break. 

**when可以一次指定多个值:** 

```ruby
tags = ['A', 'IMG', 'PRE']
tags.each do |tagname|
	case tagname
	when "P", "A", "I", "B", "BLOCKQUOTE": 
		puts "#{tagname} has child"
	when "IMG", "BR" 
		puts "#{tagname} has no child "
	else
		puts "#{tagname} cannot be used"
end 

```

**when用来判断类型**

```ruby
array = ["a", 1, nil]

array.each do |item|
	case item
	when String
		puts "item is a string"
	when Numeric
		puts "item is a numeric"
	else 
		puts "item is something"
end 

```
本例中判断的主体不是item, 而是item所属的类. 

**使用正则表达式的匹配结果来进行不同的处理** 

```ruby
text.each_line do |line|
	case line
	when /^From:/i 
		puts "发现寄信人信息"
	when /^To:/i
		puts "发现收信人信息"
	when /^Subject:/i
		puts "发现主题信息"
	when /^$/
		puts "头部解析完毕"
		exit
	else 	
	end 
```

**总结: ===与case语句**

在case语句中 when判断值是否相等时, 实际使用===运算符来判断. 

+ 左边是数值或者字符串时, ===与==的意义是一样的
+ 除此之外, ===还可以与+~一样用来判断正则表达式是否匹配, 或者判断右边的对象是否属于左边的类. 
+ 对比单纯的判断两边是否相等, ===能表达更加广泛的"相等"

```ruby
p (/zz/ === 'xyzzy') # => true
p (String === "xyzzy") # => true
p (1..3 === 2)  # => true

case value 
when A
	puts "A"
when B
	puts "B"
else 
	puts "C"	
end 

if A === value 
	puts "A"
elseif B === value
	put "B" 
else
	puts "C"
end  
```
请注意when指定的对象在===的左边

**对象的统一性**

所有的对象都有标识的值
标识(ID)用来表示对象的同一性, ruby中所有对象都是唯一的, 对象的ID可以通过object_id(或者__id__)方法获得

```ruby
arr1 = []
arr2 = []
p arr1.object_id
p arr2.object_id 

```
使用`equals?`方法来判断两个对象是否是同一对象(ID是否相同)

```
str1 = "foo"
str2 = str1 
str3 = "f" + "o" + "o"

p str1.equals?(str2)  # => true
p str1.equals?(str3)
```