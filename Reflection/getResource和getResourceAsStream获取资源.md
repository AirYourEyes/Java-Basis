## 一、项目目录结构
1. URL getResource(String name)方法  
先看以下代码
```
	System.out.println(Test.class.getResource(""));
	System.out.println(Test.class.getResource("/"));
```
上面的代码输出为：  
```
file:/D:/Java/workspace/Test/bin/testpackage/
file:/D:/Java/workspace/Test/bin/
```
从上面的代码我们可以得出以下的结论：
  - name不以反斜杠开头的表示从当前类所在的包开始寻找资源
  - name以反斜杠开头的表示从包含该类所在的包的目录开始寻找资源,
2. InputStream getResourceAsStream(String name)方法
	- 只有