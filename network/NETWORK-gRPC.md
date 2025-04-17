# gRPC


### RPC
- <span style="color:green;font-weight:bold">R</span>emote
<span style="color:green;font-weight:bold">P</span>rocedure
<span style="color:green;font-weight:bold">C</span>all의 약자
로 이름에서 알 수 있듯 다른 컴퓨터에 있는 어떤 기능을 자기 기능인 것처럼 실행할 수 있도록 하는 프로토콜
- RPC는 언어 독립적이므로 서로 다른 프로그래밍 언어를 사용하는 서버와 클라이언트 상이에서도 사용될 수 있음
#### [Server(Ruby)]
```Ruby
require 'xmlrpc/server'

def add(a,b)
   return a+b
end

server = XMLRPC::Server.new(8080)
server.add_handler("sample.add") {|a,b| add(a,b)}
server.serve
 ```
#### [Client(C#)]
```C#
using System;
using CookComputing.XmlRpc;

public interface IAdditionStub : IXmlRpcProxy{
   [XmlRpcMethod("sample.add")]
   int Add(int a, int b);
}

class Program{
   static void Main(string[] args){
       IAdditionStub stub = XmlRpcProxyGen.Create<IAdditionStub>();
       stub.URL = "http://localhost:8080/";

       int result = stub.Add(5,3);

       Console.WriteLine("5 + 3 = " + result);
   }
}
```

### gRPC
- 구글에서 만든 RPC 프레임워크
- 프로토콜 버퍼를 사용해 서버와 클라이언트가 데이터를 주고받음
- HTTP2를 사용하기 때문에 멀티플렉싱을 사용할 수 있음
- TLS를 이용해 데이터를 암호화

##### json vs proto
![json vs proto](/network/img/NETWORK-gRPC_json_proto.jpg)