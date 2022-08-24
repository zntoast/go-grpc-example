# go-grpc-example

#### Go-gRPC Windows环境安装

1、安装 protobuf

> 下载地址：[https://github.com/protocolbuffers/protobuf/releases](https://github.com/protocolbuffers/protobuf/releases)
>
> 选择win64的压缩包

2、将解压好的protoc.exe放到 goPath/bin目录下

在控制台输入 protoc --version 显示版本号则表示安装成功

3、将protobuf文件编译成golang文件还需要用到两个插件

> go mod init go-grpc-example
>
> go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2
>
> go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28

在goPath/bin 目录存在protoc-gen-go.exe 和protoc-gen-go-grpc.exe 则表示安装成功

4、新建文件夹proto

```
创建 helloworld.proto 文件

// 版本号
syntax = "proto3";

// 输出路径 mod + 相对路径地址
option go_package = "go-grpc-example/proto";
// 报名
package helloworld;

// 创建 rpc 服务
service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// 请求服务
message HelloRequest {
  string name = 1;
}

// 响应请求
message HelloReply {
  string message = 1;
}
```

5、编译 proto 文件

```
 protoc --go_out=. --go_opt=paths=source_relative   --go-grpc_out=. --go-grpc_opt=paths=source_relative   要编译的目标文件
 
 例 : protoc --go_out=. --go_opt=paths=source_relative   --go-grpc_out=. --go-grpc_opt=paths=source_relative ./proto/helloworld.proto
```

6、安装所需的SDK包

> 编译好文件后发现缺少SDK可以直接 go mod tidy
>
> 所需的依赖包有
>
> go get -u github.com/golang/protobuf/protoc-gen-go
>
> go get -u github.com/golang/protobuf/proto
>
> go get -u google.golang.org/grpc
