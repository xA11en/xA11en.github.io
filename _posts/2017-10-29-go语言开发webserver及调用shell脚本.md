---
layout: post
title: go语言开发webserver及调用shell脚本
date: 2017-10-29
tag: 开发语言
---



### 博文编写背景
由于需要对压测系统的被压服务进行进程监控，多方面考虑后go语言的运行环境不依赖任何类库，直接编译成二进制包就可以在linux执行，非常方便，固有了以下博文，有不对的地方还大家可以一起讨论更正

### go语言背景介绍
Go语言是谷歌2009年发布的第二款开源编程语言。Go语言专门针对多处理器系统应用程序的编程进行了优化，使用Go编译的程序可以媲美C或C++代码的速度，而且更加安全、支持并行进程。北京时间2010年1月10日，Go语言摘得了TIOBE公布的2009年年度大奖。Go语言设计支持主流的32位和64位的x86平台，同时也支持32位的ARM架构。谷歌资深软件工程师罗布·派克(Rob Pike)表示，“Go让我体验到了从未有过的开发效率。2013年5月07日，Go语言Go 1.1RC2版发布。Vim是从vi发展出来的一个文本编辑器，代码补全、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用（原文来自百度百科，详情自己搜索）
话不多说，直接进入正题吧

### go_linxu环境安装
 - go语言linux环境包下载（https://golang.org/dl/    go1.9.2.linux-amd64.tar.gz ）
 - 下载后选择你喜欢的位置解压,并且配置go语言的环境变量，为了你的环境变量有可能重启shell 不生效 建议写在文件里（**vim /root/.bashrc**）
 - 通过go version测试你的环境是否生效，一切ok后就可以开发一个webserver

### go webserver开发及如何调用shell
话继续不多说，直接上代码吧

{% highlight elang %}
package main  
import (  
    "encoding/json"  
    "fmt"  
    "net/http"  
    "log"
    "os"
    "os/exec" 
)  
 // 定义返回json结构体
type BaseJsonBean struct {  
    Code    int         `json:"Code"`  
    Message string      `json:"Message"`  
}  
 // 返回json对象
func NewBaseJsonBean() *BaseJsonBean {  
    return &BaseJsonBean{}  
}

//检查函数异常错误
func checkErr(err error) {
	if err != nil {
		log.Println(err)
	}
}
 
func WebServerBase() {  
    var i,p = "xxxxxxx","xxxx"
    log.Println("api  [ getRelayRunStatus  ]monitor relay run staus is start... server is ",i+":"+p) 
    //第一个参数为客户端发起http请求时的接口名，第二个参数是一个func，负责处理这个请求
    http.HandleFunc("/getRelayRunStatus", moitorRelay)  
  
    //启动监听的服务ip 端口
    err := http.ListenAndServe("0.0.0.0:"+p, nil)  
    checkErr(err)  
}  
 // 具体的接口功能实现 
func moitorRelay(w http.ResponseWriter, req *http.Request) {  
    log.Println("moitorRelay is running...") 
    //req.ParseForm()
    result := NewBaseJsonBean()
    if req.Method == "GET"{
	result.Code = 2001
        result.Message = "warning: request method must be post"
        bytes, _ := json.Marshal(result)
        //返回response 的json数据
        fmt.Fprint(w,string(bytes))
        return
    }else{
	ip := req.FormValue("ip")
	port  := req.FormValue("port")
	log.Println(ip,port)
	if ip == "" || port == "" {  
		result.Code = 2001 
		result.Message = "error:parameters is null "
		bytes, _ := json.Marshal(result) 
		fmt.Fprint(w, string(bytes))
		return
	}
	//处理shell脚本每次重新写入shell内容
	f, err := os.OpenFile("monitor_relay.sh", os.O_WRONLY|os.O_TRUNC, 0600)
	defer f.Close() 
	f.WriteString("netstat -nlpt | grep "+ip+" | grep "+port)
	if err != nil {fmt.Println(err.Error())}
	//调用脚本并返回脚本的返回值
	cmd, err := exec.Command("/bin/sh", "./monitor_relay.sh").Output()
	var str = string(cmd)
	if str == ""{
		result.Code = 2000
		result.Message = "success:relay is core"
		bytes, _ := json.Marshal(result)
		fmt.Fprint(w, string(bytes))
		return
	}else{
		result.Code = 2002
		result.Message = "success:relay not core "+str
		bytes, _ := json.Marshal(result)
		fmt.Fprint(w, string(bytes)) 
		return
		}
    }
    
 
}
//主函数调用 main方法
func main(){

	WebServerBase()
}
{% endhighlight %}
**这里我想强调的是，go在处理shell脚本时并且传参到shell脚本时是通过每次重新覆盖shell脚本文件的方式，先生成shell文件在通过go来调用的**

### 参考文献
 - http://www.yiibai.com/go/
 - https://studygolang.com/articles/4846

### 作者信息
- QQ:294040201
