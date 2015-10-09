## 关于编译或目录
1. 设置`GOROOT`或`GOPATH`，一般设置后者，这样`go build`时即会从这些路径里优先读取

2. 要在主程序里应用本项目或其它项目的类或接口时，必须先把其它类或接口先用`go install`将其装成可引用的编译文件

	> 其中应用注意的是`go install`是针对包的，即把整个文件里所有的接口都会编译，如：`go install test/myFunc`,
	> 这里的`test/myFunc`是在整个目录结构里的`src`目录下
	
3. 对带有`main`函数的类包进行`go install`时会在`bin`目录下生成相应的可执行文件，否则会在`pkg`下生成可引用的中间文件

	> 这里应该注意的是`go install`带有main函数的主类时，会把相关的引用类一起编译并安装。
	
4. 包的引用顺序今次是`GOROOT`、`GOPATH`里的路径，如：`main.go`里引用`import test/myfunc`这时会依次从`GOPATH`和
   `GOPATH`里寻找`src/test/myfunc`,若一个环境变量里有多个路径，则依次从其中寻找，直到找到`src/test/myfunc`
   
   > 如：`GOPATH="/user/test/a:/user/test/b"`，若`user/test/a`和`/user/test/b`中都有`src/test/myfunc`,则从
   > `/user/test/a`中读取，因为其顺序靠前
