# Pet project gRPC-Quest - The Quest of gRPC
## _Abstract_
_REST_, _gRPC_ and _GraphQL_ are the three ubiquitous API technologies. There have been articles [1, 2] comparing the three, and suggesting when to use which.

Following my pet project of retrieving articles in RESTful API [3], this project is about evaluating _gRPC_. gRPC also known as Google Remote Procedure Call is an open source remote procedure call system initially developed at Google in 2015 as the next generation of the RPC infrastructure Stubby.

## _Libraries in Use_
| Library/Tool | Description | Version | 
|:-----------------|:-------:|-----------|
| protoc/libprotoc | Proto Buf Compiler | v3.19.4 |
| grpc_go | grpc with Golang | v1.43.0 |

## _Tools in use_
| Tool | Description | Version | 
|:-----------------|:-------:|-----------|
| VS Code | Microsoft Visuals Studio Code as IDE |  v1.63.2  |
| Gitbash | Git command emulator under Windows environment | v2.23.0.windows.1 |

## _Workflow_
![gRPC Workflow](image/gRPC-Workflow.png "gRPC Workflow")<br/>
_<def>_ stands for the project name, in this pet project, it's _helloworld_.
  
### Defining Service
The first step is to define _gRPC service_ and methods of _request_ and _response_ types using _protocol_ buffers. All these are defined in _.proto_ file. 

### Compiling Protocol Buffer to Generate Code
Issue following command to generate code
<pre>
$ protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    helloworld/helloworld.proto
</pre>    
It tells,
- where to get .proto file as input;
- via option _go_out_, the resultant _**&lt;def&gt;.pb.go**_ output file will be placed at the same folder relaive to input source, via option _go_opt_; and
- via option _go-grpc_out_, the resultant _**&lt;def&gt;&lowbar;grpc.pb.go**_ output file will be placed at the same directory relaive to input source, via option _go-grpc_opt_.<br/>
Note: _<def>_ stands for the project name, in this pet project, it's _helloworld_.
  
### Implementation
Folders _greeter_client_ and _greeter_server_ contain client and server codes that integrate message types and methods generated in resultants _**&lt;def&gt;.pb.go**_ and _**&lt;def&gt;&lowbar;grpc.pb.go**_.
  
## _Execution_
### Server side
At VS Code's Terminal, or a GitBash terminal, change to folder _greeter_server_ and execute following command to start server service<br/>
<pre>go run main.go</pre>
Upon execution, should see message similiar to as follows, except the date/time stamp
<pre>
PS C:\Users\user\workspace\grpc-go\examples\helloworld\greeter_server> go run main.go   
2022/02/09 06:43:05 server listening at 127.0.0.1:50051
</pre>
Again, once at client side a request is sent, expect to see following message, except date/time stamp.
<pre>$ 2022/02/09 06:44:27 Received: gRPC Trial - HelloWorld</pre>

### Client side
At another GitBash terminal, change to folder _greeter_client_ and execute following command to start client request<br/> 
<pre>go run main.go</pre>
Upon execution, should see message similiar to as follows, except the date/time stamp.
<pre>$ 2022/02/09 06:44:27 Greeting: Hello gRPC Trial - HelloWorld</pre>

## _Issue_
- Inconsistence between in-command help message of _proto_ and introductory artice, such as [4, 5].<br/>
  In the in-command help message, there is no mentioning of options _go_out_, nor _go-grpc_out_.
  
## _References_
[1] https://www.infoq.com/podcasts/api-showdown-rest-graphql-grpc/?utm_source=email&utm_medium=toppodcasts&utm_campaign=newsletter&utm_content=01252022<br/>
[2] https://www.itechart.com/blog/performance-begins-with-design-style/<br/> 
[3] https://github.com/SpenserKao/article_REST<br/>
[4] https://grpc.io/docs/languages/go/basics/<br/>
[5] https://grpc.io/docs/languages/go/quickstart/
  
