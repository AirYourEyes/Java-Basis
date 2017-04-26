## 一、简介：
- jar使用zip文件格式打包多个文件

## 二、常见的命令
|操作|命令|
|-----|-----|
|创建jar文件|jar cf jar-file input-file(s)|
|查看jar文件|jar tf jar-file|
|抽取jar文件的内容|jar xf jar-file|
|从jar文件中抽取特定的内容|jar xf jar-file archived-file(s)|
|运行打包为jar文件的应用程序（需要Main-Class头部）|java -jar app.jar|

## 三、创建jar文件
- 命令: jar cf jar-file input-file(s)
  - c表示你想要创建jar文件
  - f表示你要创建的文件不是输出到标准输出中而是到文件当中
  - jar-file表示创建的jar文件名，以.jar结尾
  - input-file(s)表示的是要打包的文件
  - 注意：该命令会自动产生默认的清单文件
- jar命令选项  

|选项|描述|
|----------------------------|-------------------------|
|v|创建jar文件时将在标准输出上输入详细的信息，详细信息包括加入jar文件的每一个文件的名字|
|0（零）|jar文件不需要压缩|
|M|将不产生默认清单文件|
|m|用来从已有的清单文件中创建清单文件，命令基本格式是jar cmf existing-manifest jar-file input-file(s)|
|-C|在执行该选项时，改变当前目录，并添加指定的文件|

## 四、查看jar文件中的内容
- 命令： jar tf jar-file
  - t表示的是你想要查看jar的内容列表
  - f选项表示的是从命令行中指定要查看的jar文件
  - jar-file：要查看的文件的路径
  - jar文件中使用的一定是相对路径

## 五、抽取jar文件中的内容
- 命令： jar xf jar-file [archived-file(s)]
  - x表示的是你想从jar归档文件中抽取文件
  - f选项表示jar文件中的内容是在命令行指定的文件中读取，而不是从标准输入
  - jar-file(s)表示的是jar文件的路径
  - archived-file(s)表示的是要抽取的文件列表，当不指明时，默认抽取所有的文件

## 六、更新jar文件
- 当你修改了清单文件或添加文件时，可使用jar工具提供的u选项更新已存在的jar文件
- 命令： jar uf jar-file input-file(s)
	- u表示你想要更新现存的jar文件
	- f选项表示的是你想更新的jar文件内容来自命令行中指定的文件
	- jar-file表示要更新的jar文件的路径名
	- archived-file(s)表示的是要更新的文件名
	- 可以通过-C选项将更新内容调到到特定的目录下

## 七、清单文件
- 清单文件存放在META-INF/MANIFEST.MF中
- 清单文件的条目是以“头部: 值”的格式存在的，头部与冒号之间没有空格，而冒号与值之前有一空格隔开
- 清单文件必须以新的一行或者换行返回结束，否则最后一行无法正确解析
- 命令： jar cfm jar-file manifest-addition input-file(s)
  - c表示的是你想要创建jar文件
  - f表示的是你要输出到文件而不是标准输出流
  - m表示的是将你指定的文件中的内容与合并到jar文件的清单文件中
  - manifest-addition表示的是要被合并到清单文件中的内容所在的文件
  - input-file(s)表示要添加到jar文件中的所有文件，以空格分开
  - 要注意的是清单文件的编码格式一定要是utf-8
- 清单文件的写法
  - 设置应用程序的入口
      - Main-Class: classname
      - clssname是main函数的所在的类的名字（包括包名）
  - 通过jar工具设置入口点
      - JDK6后通过e标志可以创建或重写Main-Class属性
      - 可以在创建或更新jar的时候使用该标志
      - 例如：jar cfe app.jar MyApp MyApp.class创建了jar文件，并将Main-Class属性设置为MyApp
      - 如果入口类名字在包中，则需要点号（.）作为分隔。例如：若Main.class在foo包中，命令应该写成jar cfe Main.jar foo.Main foo/Main.class
  - 引用其他的jar文件
      - 格式：Class-Path： jar1-name, jar2-name, jar3-name, directory-name/jar-name
      - 使用Class-Path这种方式指定引用jar文件的路径可以避免在运行时执行冗长的-classpath标志的情况
      - Class-Path的值只能是**本地jar或类文件，不能是内嵌在jar中或者通过网络协议得到的jar或类文件。
      **例如：MyJar.jar包含MuUtils.jar文件，你不能使用MyJar.jar的清单文件来将MyUtils.jar的类文件加载到类路径当中**

