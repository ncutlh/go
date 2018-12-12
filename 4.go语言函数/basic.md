# 4.1函数

##面向过程实现方法
    func(接收器 接收器类型) 方法名（参数列表）{函数体}
    func(b *Bag) Insert(itemid int)
 ###指针类型的接收器和非指针类型的接收器
 
## 函数式编程 vs 函数指针
1、参数，变量，返回值都可以是函数

## 闭包
#![闭包](/assets/go函数闭包.png)
    func adder() func(int) int {
    	sum := 0
    	return func(v int) int {
    		sum += v
    		return sum
    	}
    }
    func main() {
    	 a := adder() is trivial and also works.
    
    }

## 正统式函数编程：（不推荐）
    type iAdder func(int) (int, iAdder)
    
    func adder2(base int) iAdder {
    	return func(v int) (int, iAdder) {
    		return base + v, adder2(base + v)
    	}
    }
    func main() {
    	// a := adder() is trivial and also works.
    	a := adder2(0)
    	for i := 0; i < 10; i++ {
    		var s int
    		s, a = a(i)
    		fmt.Printf("0 + 1 + ... + %d = %d\n",
    			i, s)
	}
    }
## 可以为函数实现接口
    func Fibonacci() func() int {
    	a, b := 0, 1
    	return func() int {
    		a, b = b, a+b
    		return a
    	}
    }