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
