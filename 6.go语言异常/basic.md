# 6.go语言异常

##defer调用
>1、确保在函数结束时调用

    func tryDefer1() {
    		defer fmt.Println(1)
    	    defer fmt.Println(2)
    		      fmt.Println(3)
    	   return
    			 fmt.Println(4)
    }


    func tryDefer1() {
    		defer fmt.Println(1)
    	    defer fmt.Println(2)
    		      fmt.Println(3)
    	   panic("ssss")
    			 fmt.Println(4)
    }
>2、什么时候调用
    Open/Close
    Lock/Unlock
    PrintHeader/PrintFooter
    
##服务器统一出错处理
##panic和recover
>1、panic 停止当前函数执行；一直向上返回，执行每一层的defer；如果没有遇见recover，程序退出
>2、recover 仅在defer调用中使用，获取Panic的值，如果无法处理，可重新Panic

## 即打印又返回异常
    func testa() {
    	fmt.Println("aaaaaaaaaaaaaaaaa")
    }
    
    func testb(x int) {
    	//设置recover
    	defer func() {
    		//recover() //可以打印panic的错误信息
    		//fmt.Println(recover())
    		if err := recover(); err != nil { //产生了panic异常
    			fmt.Println(err)
    		}
    
    	}() //别忘了(), 调用此匿名函数
    
    	var a [10]int
    	a[x] = 111 //当x为20时候，导致数组越界，产生一个panic，导致程序崩溃
    }
    
    func testc() {
    	fmt.Println("cccccccccccccccccc")
    }
    
    func main() {
    	testa()
    	testb(20)
    	testc()
    }
