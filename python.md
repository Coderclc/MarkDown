For in 遍历时如果列表或者字典改变，对应的元素位置也会改变,可以采用for a in aa.copy():就可以了遍历副本,删除正本



Def greet_user():
“””文档字符串”””描述函数的作用
位置实参注意 顺序
关键字实参数，无关顺序
如果少输入一个实参，形参要有默认值
传递列表时，实参列表切片，传的就是副本，在函数中修改副本是修改不了列表的

Def make_pizza(*toppings):元组形式的可变参数。
**字典形式的可变参数
先匹配关键字形参或位置形参，再把剩余的创建元组形参
形参默认值和形参元组也冲突了，二者都要求放在后面才行。

def users_info(first_name,last_name,**user_info):
    a={}
    a["First_name"]=first_name
    a["Last_name"]=last_name
    for key,value in user_info.items():
        a[key]=value
    return a
    
a=users_info("chen","licheng",b={"期中":90})
print(a)
a=users_info("chen","licheng",期中=90)
print(a)
bad={"期中":90}
a=users_info("chen","licheng",**bad)
print(a)
注意细节
字典形式的可变参数中，期中，左边的默认有双引号
传递字典到函数中
第一种是直接作为普通参数传进来，此时函数内改变字典，字典就改变
extra = {'city': 'Beijing', 'job': 'Engineer'}
def person(kw):
    kw['city']='qingdao'
person(extra)
print(extra)

结果：
{'city': 'qingdao', 'job': 'Engineer'}

但是字典作为可变参数时，函数内对字典修改，不会影响到原来的字典。

extra = {'city': 'Beijing', 'job': 'Engineer'}
def person(**kw):
    kw['city']='qingdao'
person(**extra)
print(extra)

结果：
{'city': 'Beijing', 'job': 'Engineer'}
函数的调用
函数在a模块中
Imoprt a
a函数（）
导入特定的函数
Froom a import 函数
函数（）
起别名
As
From a import 函数 别名
也可以给模块起别名
From a import * 插入所有函数

类的运用

先实例化（基于类创建对象），才能调用方法。
__init__ 是一种特殊的方法，每次基于类创建对象时，都会运行这个方法
Self :每个与类相关联的方法调用都自动传递实参self，
它是一个指向实例本身的引用，不然怎么区分对象/实例，让实例能够匹配到类，访问类中的属性，和方法变量都可供类中的所有方法使用
以self为前缀的

继承
子类括号要有父类，父类要在子类的前面
使用super().__init__函数，关联子类和父类
共有的属性应该加在父类，而不是子类中。
子类的方法与父类的方法重名时，执行的子类

创建类时要想不带参数，
Self后面不带形参，或者形参有默认值
要么默认值要写在形参。

class Battery():
    def __init__(self):
        battery_size=80
        self.battery_size=battery_size

class Battery():
    def __init__(self,battery_size=80):
        self.battery_size=battery_size


将实例作用于属性，再类中包含类，
每次创建A类，都自动生成B类， 模块化，清晰数据化
将会改变的形参，实参放在除__init__的方法中

Pass语句

music.isdigit()如果music除了数字字符串还有其他的,就会放回false否则返回true
理解 位置实参,关键字实参
任意数量实参, 结合任意数量的位置实参,
结合任意数量的关键字实参
每个函数都应包含文档字符串形式的注释.
参数中,形参默认值,关键字实参等号两边不要有空格.
创建子类时,父类必须在当前文件,并且在子类前面
导入多个类,用逗号隔开.
类名应该驼峰命名法.类中的单词每个字母都大写,且不用下划线
一个空行隔开方法,两个隔开类

With 关键字 在不需要访问文件后将其关闭
函数Open()接受一个参数,参数为打开文件的名称
Open()返回一个表示文件的对象.
As  将这个对象存储到后面的变量中
Close()如果未执行,将会丢失数据
Read()读取文件中的内容,并且返回,读到末尾的时候回返回一个空字符串,返回字符
相对文件路径,还在一个子文件中
Windows系统为\  linux,OS X为/
字符串前加r,消除转义标记
打开文件后的操作,要缩进	
直接遍历指向文件内容的对象,可获得每一行的内容
为了在with模块外使用内容,可用readlines()函数直接存储起来,函数的返回值是一个列表
对象.readlines()=对象
Float()转为浮点数
字符串也跟数组一样可以截取位数!!!!
print(line.rstrip().replace("Python","c"))
这种结构是成立的
Replace()函数,左参为原值,右参为更改值,临时改变
Write(“内容”)
W””只写模式,没有的时候创建文件,每次重新读取会清空内容
A 附加模式  没有回创建文件,在文件后加上内容
r只读模式,默认也为只读模式,文件不再读取不到
R+读写模式  垃圾,又要有文件,先入又会被替换
Python只能读取和写入字符串,写入数字时要先进行str转换
W ,r可以创建文件,不能创建文件夹
字符串对象访问.split（）
函数返回一个以空格为间隙隔开的数组，数组元素为一个一个单词，用len测，一个格长1
方法 对象.count(内容)返回内容在对象中出现的次数
运行错误,生成异常对象,代码进行处理.程序继续运行
Try except else  缩小捕获的对象
使用else子句比向try子句添加额外的代码要好，因为它避免了意外捕获由try...except语句保护的代码未引发的异常。使用else子句比向try子句添加额外的代码要好，因为它避免了意外捕获由try...except语句保护的代码未引发的异常。
无法精确用except监管
避免用户看到traceback，程序继续运行
Pass提醒你什么都没有做,还有以后要做什么
"""10-6加法运算"""
prompt="请输入两个数字,我会将其相加"\
       "不要输入数字以外的字符哦"
prompt1="请输入两个数字,我会将其相加"
prompt1+="不要输入数字以外的字符哦"

print(prompt)
print(prompt1)
print("请输入两个数字,我会将其相加" +
      "不要输入数字以外的字符哦")



Ctrl + Alt + L	代码格式化
Ctrl + Shift +/-	展开/折叠全部代码块
Ctrl + Y	删除当前行
Shift + Enter	换行（不用鼠标操作了）
Ctrl + Delete	删除到字符结束
Ctrl + Backspace	删除到字符开始快速删除


Alt + Shift + up/down	当前行上移或下移动
Ctrl + W	选中增加的代码块
Ctrl + /	行注释（可选中多行）
Json.dump(data,实例)
Jsom.load(实例)
进行单元测试,,测试用例为大是一组单元测试
导入单元测试模块,unittest,和要测试的函数.
创建一个子类,驼峰法命名,名字要包含test,继承unittest.Testcase类
调用函数,self.断言方法(函数生成的结果,和你想象的结果)
Unittest.main()用于测试类中以Test打头的方法,方法不是test打头不会自动运行
第一行的据点表示有一个单元测试通过了,
注意的地方,继承父类的 父类名为unittest.Testcase
self.assertEqual()断言方法
文件名为函数\模块名eg name_fuction
子类名为 测试对象 eg StringTestCase
方法名为test_加上被测函数名
测试函数就是在类中调用函数,测试类就是在类中创建对象
SetUp()先运行方法setUp再运行test打头
多语句可以用分号隔开,浮点型字符要变整形先float,再int
允许;分号隔开语句,
a = b = c = 1允许同时为多个赋值
a,b,c=1,2,’jack’



Turtle
Turtle.Pen()
 Forward()backfawrd()left()right()up()down()reset()clear()
Color(“pink”,”pink”) 线条颜色,填充颜色
Begin_fill  end_fill 填充颜色
Setheading(0)指定方向
Circle()

Time 模块 
time.asctime()
Time.time()自从1970年一月一日00.00.00AM以来的秒数用来比较值
Time.localtime()
Time.sleep()延时


sys模块
Sys.stdin.readline()可以指定读取多少个字符
Sys.stdout.write()打印
Sys.exit()

abs()返回绝对值     bool()返回True False
Dir() 返回对括号内的各种相关信息
Eval(“”)执行括号分号内的表达式
Exec 执行更复杂的函数
Copy 要先插入模块浅拷贝,,能复制多一个列表,但不能复制列表中的对象,
Keyword模块
Keyword.iskeyword(‘if’)返回true,false
Keyword.kwlist   返回所有的关键字
Random 模块  
random.randint(1,100)一到一百随机选一个数字
Random.choice()在列表随机选一个元素
Random.shuffle()洗牌
Print(“%s”%(a-b))
字符,数字,字符串可以直接复制,列表和字典不行

Enumerate()for x,y in cc
将值和索引联系
Csv中的阅读器对象遍历后会改变指针的位置,matplotlib值不按顺序排列就是字符类型问题
print("{} is month {} week{},{},the close price is {}RMB".format(date, month, week, weekday, close))
print("%s is month %s week%s , %s, the close price is %s RMB" %(date, month, week, weekday, close))
