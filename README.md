### Learning Go Note 

#### 20170602 

* Download Go from https://golang.org/ . setting Env （GOPATH/GOROOT） . in windows the default GOROOT is `C:/go` the default GOPATH is `%USERPROFILE%/go` . in unix . we should better set GOROOT to `/usr/local/go` and GOPATH to `$HOME/go`

* Download GolangIDE from JetBrain https://link.zhihu.com/?target=https%3A//www.jetbrains.com/go/ using IDE just to write code . build code now i still use command . 
```
go build // build code 
go install // install code 
go env GOROOT // using go env ## check out the value of go env variables  
```

* Read https://golang.org/doc/code.html#Workspaces 

#### 20170603

##### a tour of go

* the export variable name is uppercase 
* the syntax of go is different from c and more human . for more read https://blog.golang.org/gos-declaration-syntax
* can have multiple return value , and can have the so called naked return .
* var statment declare a variable and the type is in the last it can be defined in the function lever or package lever , when we declare a variable and initialize it , then the type can be omitted , the := can replace implicitly of var and type , but the package variable must start with var ,func and so on so the := can not be used out of func  
```go
var a ,b ,c bool
func t(){
  var d , e int
  f := "hello world"
}
```
* go basic type 
```go
bool // in java => boolean , in c bool 
string // in java => String , in c char[]
int int8 int16 int32 int64 // in java only has int , in c also not has others
uint uint8 unit16 uint32 uint64 // java do not has unsigned int type  , c only has uint .
byte // the alias of int8
rune // alias for int32 , represents a Unicode code point
float32 float64 // java has float 32bite , c has float 
complex64 complex128 // java has not such type , so is c 
// by the way go do not has char which is what int16 stand for and double is represent by float64
```
* implicit uninitialized variable value , 0 for numerics , flase for bool , "" for string 

* type conversion in java it is something like (Integer)str , in go it is like float64(str) , which way do you think is more human readable , i think it's go 

* constant declared in go is the same as in c , using const statment. const can not using := for := is dynimic define the variable type ,but the constant can not have anything to do with dynimic so .

* in go there are only one loop key word is for , there is no while , and while spelled for in go.
```go

for i:=0;i<10;i++{
  sum:+=i;
}

for i<10 { // omit the first and third statement
  // 
}

for { // omit all three statement

}
```
* if statement like for , can predefine a statement  the variable defined in pre-statement can be accessed only in if and else statement.
```go
if i:=10;i<9 {
  
}
```
* switch statement , also can start with a statement like for and if , not like java switch compare variable can be not just only int ,can also be other type like string . unlike java the switch will stop when one case is matched , then other case will not even be executed . switch with no condition is the same as switch true . this is very cool . 
```go
switch t :=1;t {
	case 0:
		fmt.Printf("hello switch 1\n")
	case 1:
		fmt.Printf("hello switch 2\n")
	default:
		fmt.Printf("hello switch 3\n")
	}
  
  t := time.Now();
	switch  {
	case t.Day() > 1:
		fmt.Printf("switch 1\n")
	case t.Day() < 1:
		fmt.Printf("switch 2\n")
	}
```
* defer . this is a new key word , there is no such key word in java or c . defer means do it later , the defer call's argument will be initialzed immediatly but execution will be the last . for more about defer and panic and recover read https://blog.golang.org/defer-panic-and-recover
```go
func testDefer(){
    defer fmt.Printf("bitch")
    fmt.Printf("hello");
}
```
* pointer . very much like c , but the declaring is not the same as we spoked before , and the pointer can not do arithmetic
```
var a *int // a is a int pointer
b := 10 
a = &b     // revalue a to b's underly location using operator & 
fmt.Println(*a) // get the value out of a using * add the variable 
```

* struct . A struct is a collection of fields. like in c . using dot to access struct field like in c , when we have a pointer struct , we can do not need to dereference the pointer then dot to the field .  declare a struct using struct literal. we can say struct is the java's entity
```
type A struct{
  a int
  b int
}
c := &A{1,2};
c.a // no need to (*c).a
```

#### 20170604
##### a tour of go
* Array in go . var a [10]int. declare a variable a as a array of  ten integer. like in java array's size is defined when we define a array . add can not be resizing.
```
b := [...]string{"Penn", "Teller"} // cool ha.
```
* dynamic array  `slice` .  the type []T is a slice with Elements of Type T.  a[0:5] indicate the first five element of array a . there is no such concept in java or c . but it is as said more common used than array . in go . so we will say about that . slices are like references to arrays . if we change the slices value the under arary data will change accordingly . other slices that share the same under array will see the same changes. slice literal are like array literal just not contains the size . slice default , the low bounds are 0 the high bounds are the length of the underly array. by the way the zero value slice is nil . creating slice with `make`  
```
arrInt:= [5]int{1,2,3,4,5} ;

sliceArr := arrInt[1:3];

fmt.Printf("%v %d \n",sliceArr,len(sliceArr))

sliceArr[0] = -1;

fmt.Printf("%v %d \n",sliceArr,len(sliceArr))

//sliceArr[2] = 100

//fmt.Printf("%v %d \n",sliceArr,len(sliceArr))
	
sliceArr1 = []bool{true,false} // the same as sliceArr1 = [2]bool{true,false}

var arr1 = arrInt[:]
	
var arr2 = arrInt[0:]

var arr3 = arrInt[:5]

fmt.Printf("%v %v %v\n" , arr1,arr2,arr3)

// test len and cap function of slice
arr1 = arr1[0:0]

fmt.Printf("len is %d , cap is %d",len(arr1),cap(arr1))

arr1 = arr1[:4]

fmt.Printf("len is %d , cap is %d",len(arr1),cap(arr1))

arr1 = arr1[2:]

fmt.Printf("len is %d , cap is %d val %v \n",len(arr1),cap(arr1),arr1)

var zeroSlice []int

fmt.Printf("len is %d , cap is %d" , len(zeroSlice), cap(zeroSlice))

makeSlice := make([]int,5) // make a zero slice of capacity and len 5
makeSlice1 := make([]int,0,5) // make a zero slice of capacity 5 and len 0  
makeSlice1 = makeSlice1[:2] // as long as we have capacity we can rearrange the length.

// slice of slice 
slice1 :=[]int{1,2,3};

slice2 := [][]int{slice1}

fmt.Printf("slice of slice is just like array of array %v",slice2)
```

* append and copy slice , read https://blog.golang.org/go-slices-usage-and-internals

* range in go , is a litter bit like iterator in java .  range can iterate array and map 
```
sliceArr := []int{1,23}
for  i,v := range sliceArr {
	fmt.Printf("index is %d , value is %d",i,v)
}
for  _,v := range sliceArr {
	fmt.Printf("value is %d",v)
}
for  i := range sliceArr {
	fmt.Printf("index is %d",i)
}

hosts := map[string]IPAddr{
	"loopback":  {127, 0, 0, 1},
	"googleDNS": {8, 8, 8, 8},
}
for name, ip := range hosts {
	fmt.Printf("%v: %v\n", name, ip)
}
```
* map in go , like there is map in java.  and we can use make function to make map too.  
```
// insert or update a map value
map["key"] = value
// get key value 
v := map["key"]
// test a key exist or not . if not exist then ok = false and v is the zero value of Type Element . 
v,ok := map["key"] 
```

* function value , like in c , functions can be arguments or returned values too.  function closure.  A closure is a function value that references variables from outside its body. The function may access and assign to the referenced variables; in this sense the function is "bound" to the variables.

* method . like in java but not defined in the class scope , for in go there is no class . method is like a function with a receiver argument . we can only declare a method with a receiver type in the same package of the method . we can not define a method with a receiver type not in the method package.  a pointer receiver consider to be a better receiver for we most often change the receiver's inner data , if it is not a pointer receiver , when we manipulate the receiver the underly type data will not change responsivily , for the receiver is just a copy of the source type. with functions , we have give exactly the arguments , but with with method , not neccesaryly . 
```

type A struct{
  a int
}

func (a A) Abs() int{
  if a < 0 {
    return -a;
  }
  return a;
}

func main(){
  a :=A{10}
  a.Abs()
  a1 := &a
  a1.Abs()
  
}

```

* interface , a interface is a type defines a list of methods signature.  a value of interface type can hold any type that implements those methods . an type implements a interface by implements its methods, there is no explicit word for that , no "implements" key word like in java or c++ , implicit implementation decouples the interface and its implementations, which could then apear in any package without prearrangement.  the interface type hold zero method called a empty interface , which can hold any type , 

```
type A interface{}

func main(){
	i := 0;
	var a A;
	a = i;
}
```

#### 20160605
`Stringer` . one of the most ubiquitous interface is stringer defined by fmt package .  it is the same as toString method in java . 
```
type Stringer interface{
  String() string
}
```
* `error` . just like Stringer it is also a build-in type .  Function often return a error . so when error happens they can execute some code by testing whether the error equals to nil .  a nil err value means success , a non nil err value means A error happened
```
type error interface {
  Error() string
}
```
* Reader . read data from stream . Reader method populates the given byte slice with data and returns the number of bytes populated and error value . it returns a io.EOF error when stream ends.
```go
func (T) Read(b []byte)(n int,err error)
```

#### 20170606

* goroutine . a light wait thread managed by Go runtime .  just like thread in java when we access the shared memory we must use synhronized . 
```go
go f(x,y,z) // start a goroutine run f . the evaluation of x , y , z in the current goroutine , the execution of f start in new goroutine . 
```

* channels is a typed conduit that we can put data and receive data from it using `<-` . like map and slice we can make channels by using make(chan ch) . By default , send and receive are block until the other side is ready . this allows goroutine synchronzed without explicity lock or condition variables.  Buffered Channels `ch := make(chan int ,100)` send to bufferd channels block when channels is full , receive from a bufferd channels block when channels is empty.
```go
ch <- v // send v into channels 
v := <- ch // receive v from channels 
```

#### 20170607

* range can use to iterator the conduit of channal receiving data from a channal . it will stop when there is when the range hit the close sign. so we can close the channel when we are done sending data into channel . it is only normal for us to close a channel on a sending data func . sending data to a close func will cause panic .  but we do not must close a chan only when the receiver must be told there will no more data comming. 
```go 
v,ok := <-ch // if no more data receive and the chan is close then ok is false 
```

* the select statement let a goroutine wait on multiple compunication operations. A select blocks untils one of its case run . it choose one randamly when multiple are ready. using default on select . can receive or send data to a channel with out block.

* hot key for mac . 
``` go 
command + o => go to any type you want . 

shift cmd + o => go to files 

alt cmd + o => symbol  

cmd + b => go to declaration 

cmd 7 => structure window 

cmd e => check recent files 

shift cmd e => recent edit files

fn + cmd +f7 => check symbol usages 

cmd +n  => code generation 

shift + cmd + A => action or option names

build-in test web service

build-in database 

build-in version controller tools
```

#### 20170608

* Read https://golang.org/doc/code.html

#### 20170618

* finishing Reading https://golang.org/doc/code.html 
* starting reading the source code of go . 

#### 20170619 
* finish reading unicode package source code ,and string package . prepared to go in the real project , watch the source code if neccessary for the efficiency consideration.


#### 20170620
* struct is like Entity in java . how to use struct ? when to use struct ? just ask yourself when i should use entity , how should i use entity . and struct also can have methods . and a bunch of methods can make a interface , just like in java. 

* []*string vs *[]string : the first one means A array of string pointer . the second one means a pointer point to a array of string . they are so not the same. 

* the Upper case letter means export , the lower case can be import in the same package.

#### 20170621
* 

#### 20170626
* what is the difference between type conversion and type assertion .
```go
// type assertion deal with interface convert underly interface into any type that it is .
	var a interface{} = int64(5)
	b := a.(int64)
	fmt.Println(b)

// type conversion just convert type .
	var c int32 = 74
	d := int64(c)
	fmt.Println(d)
```

* normally when we use struct we define a pointer to the struct . interface not so much . 

* how to convert a byte into string
```go
func byte2Str(b []byte) string {
	var varStr string
	for i:= 0 ; i <len(b);i++{
		r , _ := utf8.DecodeRune(b[i:i+1])
		varStr += string(r)
	}
	return varStr
}
```
* do you know how go implement multiple interface ?
```
type Pipeline interface {
    Process(items *page_items.PageItems, t com_interfaces.Task)
}

type CollectPipeline interface {
    Pipeline // now CollectionPipeline has Process method too . using composition over implementations
    GetCollected() []*page_items.PageItems
}
```

#### 20170628
* Module and inteface oriented program . this is not drill .

#### 20170701
* what is the difference between cookies and sessions https://stackoverflow.com/questions/6339783/what-is-the-difference-between-sessions-and-cookies-in-php . 

#### 20170717
* finish reading https://github.com/astaxie/build-web-application-with-golang

* ready write beego code .

1. finish writen beego/httplib
