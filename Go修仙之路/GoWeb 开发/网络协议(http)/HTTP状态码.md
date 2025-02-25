HTTTP状态码负责表示客户端HTTP请求的返回结果、标记服务端的处理是否正常、通知出现的错误等工作。

# 1. 状态码告知从服务端返回的请求结果

状态码的职责是当客户端向服务器发送请求时，描述返回的请求结果。

![](photo/Pasted%20image%2020241116105202.png)

状态码如 `200 OK`。
> 以3位数字和原因短语组成的

数字中的第一位指定了响应类型，以下是5种:

|     | 类型                      | 原因短语          |
| --- | ----------------------- | ------------- |
| 1XX | Informational(信息性状态码)   | 接收的请求正在处理     |
| 2XX | Success(成功状态码)          | 请求正常处理完毕      |
| 3XX | Redirection(重定向状态码)     | 需要进行附加操作以完成请求 |
| 4XX | Client Error(客户端错误状态码)  | 服务器无法处理请求     |
| 5XX | Server Error (服务端错误状态码) | 服务器处理请求错误     |

# 2. 2XX成功

`2XX` 的响应结果表明请求被正常处理了。

## 2.1 200 OK

![](photo/Pasted%20image%2020241116110421.png)

表示从客户端发来的请求在服务端被正常处理了。

## 2.2 204 No Content

![](photo/Pasted%20image%2020241116111138.png)

该状态码代表服务器接收的请求已成功被处理，但在返回的响应报文中**不含实体的主体部分**。
> 比如，当返回204响应后，浏览器显示的页面不发生更新。

一般在只需要从客户端往服务端发送信息，而对客户端不需要发送新的信息内容的情况下使用。

## 2.3 206 Partial Content

![](photo/Pasted%20image%2020241116111756.png)

该状态码表示客户端进行了范围请求，而服务器成功了执行了这部分的`GET`请求。
> 响应报文中包含由`Content-Range`指定范围的实体内容
# 3. 3XX 重定向

`3XX` 响应结果表明浏览器需要执行某些特殊的处理，以正确处理请求。

## 3.1 301 Moved Permanently

![](photo/Pasted%20image%2020241116112048.png)


永久性重定向。
该状态码表示请求的资源已被分配了新的URI，以后应使用资源现在所指得URI。

> 向下方给出的请求URI，当指定资源路径的最后忘记添加了"/"，就会产生`301`状态码。
> http://example.com/sample

## 3.2 302 Found

![](photo/Pasted%20image%2020241116112813.png)

临时重定向。
该状态码表示请求的资源已被分配了新的URI，希望用户本次能使用新的URI访问。

> 与 301状态码相似，但302状态码代表的资源不是被永久移动，只是临时性质的。
> 换句话说，已移动的资源对应的URI将来还有可能发生改变。

## 3.3 303 See Other

![](photo/Pasted%20image%2020241116144720.png)

该状态码表示由于请求对应的资源存在着另一个URI，应使用GET方法定向获取请求的资源。

> 303 状态码和 302 Found 状态码有着相同的功能，但 303 状态码明确表示客户端应当采用 GET 方法获取资源。
> 
  比如，当使用 POST 方法访问 CGI 程序，其执行后的处理结果是希望客户端能以 GET 方法重定向到另一个 URI 上去时，返回 303 状态码。虽然 302 Found 状态码也可以实现相同的功能，但这里使用 303状态码是最理想的。

## 3.4 304 Not Modified

![](photo/Pasted%20image%2020241116145218.png)


服务端允许请求访问资源，但未满足条件的情况。
304状态码返回时，不包含任何响应的主体部分。
> 304虽然被划分在3XXl类型中，但是和重定向没有关系。


## 3.5 307 Temporary Redirect

临时重定向。
307 会遵照浏览器标准，不会从POST变成GET。但是，对于处理响应时的行为，每种浏览器可能出现不同的情况。

# 4. 4XX 客户端错误

4XX 的响应结果表明客户端是发生错误的原因所在。

## 4.1 400 Bad Request

![](photo/Pasted%20image%2020241116150128.png)


该状态码表示请求报文中存在语法错误。
另外，浏览器会像 200 OK 一样对待该状态码。

## 4.2 401 Unauthorized

![](photo/Pasted%20image%2020241116150254.png)

该状态码表示发送的请求需要有通过 HTTP 认证(BASIC 认证、DIGEST 认证)的认证信息。若用户认证失败，则也会返回 401。

> 返回含有 401 的响应必须包含一个适用于被请求资源的 WWW-Authenticate 首部用以质询（challenge）用户信息。当浏览器初次接收到 401 响应，会弹出认证用的对话窗口。

## 4.3 403 Forbidden

![](photo/Pasted%20image%2020241116150605.png)

该状态码表明对请求资源的访问被服务器拒绝。

> 403 的原因可能是未获得文件系统的访问授权、访问权限出现了某些问题等等。

## 4.4 404 Not Found

![](photo/Pasted%20image%2020241116150812.png)

该状态码表示，服务器上无法找到请求的资源。
除此之外，也可以在服务器端拒绝请求且不想说明理由时使用。

# 5. 5XX 服务器错误

5XX 的响应结果表明服务器本身发生错误。

## 5.1 500 Internal Server Error

![](photo/Pasted%20image%2020241116151016.png)

该状态码表明服务端在执行请求时发生了错误。

## 5.2 503 Service Unavailable

![](photo/Pasted%20image%2020241116151125.png)

该状态码表明服务器暂时处于超负载或正在进行停机维护，现在无法处理请求。
