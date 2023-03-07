## 1. http/1.1 协议中与 chunked 编码的相关字段

### 1）Entity Body

`entity-body` 只有在 `message-body` 出现时才会出现。通过对 `message-body` 的解码获得 `entity-body`。`transfer-encoding` 用于确保安全和信息的恰当传输。
     `Entity-length`：在应用任何 `transfer-encoding` 之前的 `message-body` 的长度。即没有编码之前 `message-body` 的长度。

### 2）Content-length

用于描述 HTTP 消息实体的传输长度。（ the transfer-length of the message-body）

> 消息实体长度：即 `Entity-length`，==压缩前==的 `message-body` 的长度
> 
> 消息实体的传输长度：`Content-length`，==压缩后==的 `message-body`的长度。

### 3）Message Length

在具体的HTTP交互中，客户端获取消息长度主要基于以下几个规则：

- `Content-Length` 如果存在并且有效的话，则必须和消息内容的传输长度完全一致。
- 如果存在 `Transfer-Encoding`（重点是`chunked`），则在`header`中不能有`Content-Length`，有也会被忽视。
- 如果采用短连接，则直接可以通过服务器关闭连接来确定消息的传输长度。

结合 HTTP 协议其他的特点，比如说 Http1.1 之前的不支持 `keep alive`。那么可以得出以下结论：

1、在 Http 1.0 及之前版本中，`content-length` 字段可有可无。

2、在 http1.1 及之后版本。如果是 `keep alive`，则 `content-length` 和 `chunk` 必然是二选一。若是非 `keep alive`，则和 http1.0 一样。`content-length` 可有可无。

### 4）content-length字段的作用

`Content-Length` 表示实体内容长度， **客户端（服务器）可以根据这个值来判断数据是否接收完成**。但是如果消息中没有 `Content-Length`，那该如何来判断呢？又在什么情况下会没有 `Content-Length` 呢？

1. 静态页面或者图片：当客户端向服务器请求一个静态页面或者一张图片时，服务器可以很清楚的知道内容大小，然后通过 `Content-length` 消息首部字段告诉客户端 需要接收多少数据。
2. 动态页面： 如果是动态页面等时，服务器是不可能预先知道内容大小，这时就可以使用 `Transfer-Encoding：chunk` 模式一边产生数据，一边发给客户端。

## 2.chunked编码

### 1）定义

分块传输编码（Chunked transfer encoding）是超文本传输协议（HTTP）中的一种数据传输机制，允许HTTP由网页服务器发送给客户端应用（ 通常是网页浏览器）的数据可以分成多个部分。分块传输编码只在HTTP协议1.1版本（HTTP/1.1）中提供。

### 2）说明

通常，HTTP应答消息中发送的数据是整个发送的，`Content-Length`消息头字段表示数据的长度。数据的长度很重要，因为客户端需要知道哪里是应答消息的结束，以及后续应答消息的开始。然而，使用分块传输编码，数据分解成一系列数据块，并以一个或多个块发送，这样服务器可以发送数据而不需要预先知道发送内容的总大小。

### 3）格式

如果一个HTTP消息（请求消息或应答消息）的 `Transfer-Encoding`消息头的值为`chunked`，那么，消息体由数量未定的块组成，并==以最后一个大小为 0 的块为结束==。
每一个非空的块都以该块包含数据的字节数（字节数以十六进制表示）开始，跟随一个 `CRLF`（回车及换行），然后是数据本身，最后块`CRLF` 结束。在一些实现中，块大小和 `CRLF` 之间填充有白空格（`0x20`）。
最后一块是单行，由块大小（0），一些可选的填充白空格，以及`CRLF`。最后一块不再包含任何数据，但是可以发送可选的尾部，包括消息头字段。
消息最后以 `CRLF` 结尾。

[http协议中content-length 以及chunked编码分析](https://blog.csdn.net/yankai0219/article/details/8269922)