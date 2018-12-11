# 5.1接口

## 接口的定义 type 名字er interface{tt()}
1、习惯以er结尾
2、只有方法声明，没实现，没数据

    //定义接口类型
    type Humaner interface {
    	//方法，只有声明，没有实现，由别的类型（自定义类型）实现
    	sayhi()
    }
## 使用

    type Student struct {
    	name string
    	id   int
    }
    
    //Student实现了此方法
    func (tmp *Student) sayhi() {
    	fmt.Printf("Student[%s, %d] sayhi\n", tmp.name, tmp.id)
    }
    
    type Teacher struct {
    	addr  string
    	group string
    }
    
    //Teacher实现了此方法
    func (tmp *Teacher) sayhi() {
    	fmt.Printf("Teacher[%s, %s] sayhi\n", tmp.addr, tmp.group)
    }
    
    type MyStr string
    
    //MyStr实现了此方法
    func (tmp *MyStr) sayhi() {
    	fmt.Printf("MyStr[%s] sayhi\n", *tmp)
    }
    func main() {
    	//定义接口类型的变量
    	var i Humaner
    
    	//只是实现了此接口方法的类型，那么这个类型的变量（接收者类型）就可以给i赋值
    	s := &Student{"mike", 666}
    	i = s
    	i.sayhi()
    
    	t := &Teacher{"bj", "go"}
    	i = t
    	i.sayhi()
    
    	var str MyStr = "hello mike"
    	i = &str
    	i.sayhi()
    
    }
    
## 多态
    //定义一个普通函数，函数的参数为接口类型
    //只有一个函数，可以有不同表现，多态
    func WhoSayHi(i Humaner) {
    	i.sayhi()
    }
    
    func main() {
    	s := &Student{"mike", 666}
    	t := &Teacher{"bj", "go"}
    	var str MyStr = "hello mike"
    
    	//调用同一函数，不同表现，多态，多种形态
    	WhoSayHi(s)
    	WhoSayHi(t)
    	WhoSayHi(&str)
    
    	//创建一个切片
    	x := make([]Humaner, 3)
    	x[0] = s
    	x[1] = t
    	x[2] = &str
    
    	//第一个返回下标，第二个返回下标所对应的值
    	for _, i := range x {
    		i.sayhi()
    	}
    
    }
    
## 继承
    type Humaner interface { //子集
    	sayhi()
    }
    
    type Personer interface { //超集
    	Humaner //匿名字段，继承了sayhi()
    	sing(lrc string)
    }
    
    type Student struct {
    	name string
    	id   int
    }
    
    //Student实现了sayhi()
    func (tmp *Student) sayhi() {
    	fmt.Printf("Student[%s, %d] sayhi\n", tmp.name, tmp.id)
    }
    
    func (tmp *Student) sing(lrc string) {
    	fmt.Println("Student在唱着：", lrc)
    }
    
    func main() {
    	//定义一个接口类型的变量
    	var i Personer
    	s := &Student{"mike", 666}
    	i = s
    
    	i.sayhi() //继承过来的方法
    	i.sing("学生哥")
    }
    
## 接口的转换： 超集可以转换为子集，反过来不可以
    type Humaner interface { //子集
    	sayhi()
    }
    
    type Personer interface { //超集
    	Humaner //匿名字段，继承了sayhi()
    	sing(lrc string)
    }
    
    type Student struct {
    	name string
    	id   int
    }
    
    //Student实现了sayhi()
    func (tmp *Student) sayhi() {
    	fmt.Printf("Student[%s, %d] sayhi\n", tmp.name, tmp.id)
    }
    
    func (tmp *Student) sing(lrc string) {
    	fmt.Println("Student在唱着：", lrc)
    }
    
    func main() {
    	//超集可以转换为子集，反过来不可以
    	var iPro Personer //超集
    	iPro = &Student{"mike", 666}
    
    	var i Humaner //子集
    
    	//iPro = i //err
    	i = iPro //可以，超集可以转换为子集
    	i.sayhi()
    
    }
## 空接口万能类型，保存任意类型的值
    func xxx(arg ...interface{}) {
    
    }
    
    func main() {
    	//空接口万能类型，保存任意类型的值
    	var i interface{} = 1
    	fmt.Println("i = ", i)
    
    	i = "abc"
    	fmt.Println("i = ", i)
    }