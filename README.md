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
* 
