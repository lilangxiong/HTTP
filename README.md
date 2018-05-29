## HTTP：HyperText Transfer Protocol，超文本传输协议 。
### HTTP 是一种不保存状态，即无状态（stateless）协议。HTTP 协议自身不对请求和响应之间的通信状态进行保存。
```
    为了实现期望的保持状态功能，于是引入了Cookie 技术。
    有了 Cookie 再用 HTTP 协议通信，就可以管理状态了。
```
## HTTP 方法
- GET ：获取资源。
<div>
    <img src="./images/http_get.png">
</div>

- POST：传输实体主体。
<div>
    <img src="./images/http_post.png">
</div>

- PUT：传输文件（鉴于 HTTP/1.1 的 PUT 方法自身不带验证机制，任何人都可以上传文件 , 存在安全性问题，因此一般的 Web 网站不使用该方法）。
<div>
    <img src="./images/http_put.png">
</div>

- HEAD：获得报文首部（HEAD 方法和 GET 方法一样，只是不返回报文主体部分。用于确认URI 的有效性及资源更新的日期时间等）。
<div>
    <img src="./images/http_head.png">
</div>

- DELETE：删除文件（HTTP/1.1 的 DELETE 方法本身和 PUT 方法一样不带验证机制，所以一般的 Web 网站也不使用 DELETE 方法）。
<div>
    <img src="./images/http_delete.png">
</div>

- OPTIONS：用来查询针对请求 URI 指定的资源支持的方法。
<div>
    <img src="./images/http_options.png">
</div>

- TRACE： 是让 Web 服务器端将之前的请求通信环回给客户端的方法。
- CONNECT 要求在与代理服务器通信时建立隧道，实现用隧道协议进行 TCP 通信（主要使用 SSL（Secure Sockets Layer，安全套接层）和 TLS（Transport Layer Security，传输层安全）协议把通信内容加密后经网络隧道传输）。

## Cookie
```
    * Cookie 的作用是通过在请求、响应报文中写入 Cookie 信息来控制客户端的状态。
    * 在服务器端发送响应报文时通过手部字段 Set-Cookie，通知客户端保存Cookie。
    * 客户端向服务器端发送请求时会在请求报文中加入Cookie。
    * 服务器端收到Cookie时会对比服务器上的记录，最后得到之前的状态信息。
```
## HTTP报文
- 请求报文：请求端（客户端）的HTTP 报文。
<div>
    <img src="./images/http_request.png">
</div>

- 响应报文：响应端（服务器端）的HTTP 报文。
<div>
    <img src="./images/http_response.png">
</div>

- 请求报文和响应报文的首部内容由以下数据组成。
```
    1、请求行-包含用于请求的方法，请求 URI 和 HTTP 版本。
    2、状态行-包含表明响应结果的状态码，原因短语和 HTTP 版本
    3、首部字段-包含表示请求和响应的各种条件和属性的各类首部。
```

## 四种首部字段类型
### 通用首部字段：请求报文和响应报文两方都会使用的首部。
<div>
    <img src="./images/http_generalHeader.png">
</div>

1、Cache-Control: private, max-age=0, no-cache   ，格式如左。
- 请求指令：
<table>
    <tr>
        <th>指令</th>
        <th>参数</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>no-cache</td>
        <td>无</td>
        <td>表示客户端将不会接收缓存过的响应。于是，“中间”的缓存服务器必须把客户端请求转发给源服务器。</td>
    </tr>
    <tr>
        <td>no-store</td>
        <td>无</td>
        <td>暗示请求（和对应的响应）或响应中包含机密信息，规定缓存不能在本地存储请求或响应的任一部分</td>
    </tr>
    <tr>
        <td>max-age=[second]</td>
        <td>必需</td>
        <td>代表资源保存为缓存的最长有效时间（HTTP 1.1 中优先级高于Expires，HTTP 1.0 中优先级低于Expires）</td>
    </tr>
    <tr>
        <td>max-stale( = [ 秒]) </td>
        <td>可省略</td>
        <td>没有参数值，无论多起多长时间，客户端都会接收响应；有具体参数值，仍在 max-stale指定的时间内，客户端也会接收响应</td>
    </tr>
    <tr>
        <td>min-fresh=[second]</td>
        <td>必需</td>
        <td>要求缓存服务器返回至少还未过指定时间的缓存资源</td>
    </tr>
    <tr>
        <td>no-transform</td>
        <td>无</td>
        <td>无论是请求还是响应，缓存都不能改变实体主体的媒体类型</td>
    </tr>
    <tr>
        <td>only-if-cached</td>
        <td>无</td>
        <td>从缓存获取资源，如果缓存服务器的本地缓存无响应，则会返回504</td>
    </tr>
</table>

- 响应指令：
<table>
    <tr>
        <th>指令</th>
        <th>参数</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>public</td>
        <td>无</td>
        <td>缓存服务器会对任意用户提供资源缓存的服务</td>
    </tr>
    <tr>
        <td>private</td>
        <td>可省略</td>
        <td>缓存服务器会对特定用户提供资源缓存的服务</td>
    </tr>
    <tr>
        <td>no-cache</td>
        <td>可省略</td>
        <td>存服务器不能对资源进行缓存。源服务器以后也将不再对缓存服务器请求中提出的资源有效性进行确认，且禁止其对响应资源进行缓存操作</td>
    </tr>
    <tr>
        <td>no-store</td>
        <td>无</td>
        <td>暗示请求（和对应的响应）或响应中包含机密信息，规定缓存不能在本地存储请求或响应的任一部分</td>
    </tr>
    <tr>
        <td>no-transform</td>
        <td>无</td>
        <td>无论是请求还是响应，缓存都不能改变实体主体的媒体类型</td>
    </tr>
    <tr>
        <td>must-revalidate</td>
        <td>无</td>
        <td>代理会向源服务器再次验证：即将返回的响应缓存目前是否仍然有效（优先级高于 max-stale）</td>
    </tr>
    <tr>
        <td>proxy-revalidate</td>
        <td>无</td>
        <td>所有的缓存服务器在返回响应之前，必须再次验证缓存的有效性</td>
    </tr>
    <tr>
        <td>max-age=[second]</td>
        <td>必需</td>
        <td>代表资源保存为缓存的最长有效时间（HTTP 1.1 中优先级高于Expires，HTTP 1.0 中优先级低于Expires）</td>
    </tr>
    <tr>
        <td>s-maxage=[second]</td>
        <td>必需</td>
        <td>公共缓存服务器响应的最大Age值（优先级高于 Expires 、max-age）</td>
    </tr>
</table>

2、Connect 的作用：
- 控制不在转发给代理的手部字段，格式：Connection: 不再转发的首部字段名
- 管理持久连接（HTTP 1.1默认是持久连接），格式： Connection: Keep-Alive(或者 close)
    
3、Pragma 是 HTTP/1.1 之前版本的历史遗留字段，只用在客户端发送的请求中。客户端会要求所有的中间服务器不返回缓存的资源。一般与Cache-Control同时使用：
- Cache-Control: no-cache
- Pragma: no-cache

4、Transfer-Encoding 规定了传输报文主体时采用的编码方式。HTTP/1.1 的传输编码方式仅对分块传输编码有效：Transfer-Encoding: chunked。


### 请求首部字段：从客户端向服务器端发送请求报文时使用的首部。
<div>
    <img src="./images/http_requestHeader.png">
</div>

1、Accept，格式：Accept: text/html,application/xhtml+xml,application/xml;
- 文本文件：text/html, text/plain, text/css ... ；application/xhtml+xml, application/xml ...
- 图片文件：image/jpeg, image/gif, image/png ...
- 视频文件：video/mpeg, video/quicktime ...
- 应用程序使用的二进制文件：application/octet-stream, application/zip ...

2、Accept-Charset，格式：Accept-Charset: iso-8859-5, unicode-1-1;q=0.8

3、Accept-Encoding，格式：Accept-Encoding: gzip, deflate
- gzip       由文件压缩程序 gzip（GNU zip）生成的编码格式
- compress   由 UNIX 文件压缩程序 compress 生成的编码格式
- deflate    组合使用 zlib 格式（RFC1950）及由 deflate 压缩算法（RFC1951）生成的编码格式
- identity   不执行压缩或不会变化的默认编码格式
- \*          指定任意的编码格式

4、Accept-Language，格式：Accept-Language: zh-cn,zh;q=0.7,en-us,en;q=0.3

5、Authorization，格式：Authorization: Basic dWVub3NlbjpwYXNzd29yZA==
- 通常，想要通过服务器认证的用户代理会在接收到返回的401 状态码响应后，把首部字段 Authorization 加入请求中。

6、If-Match，格式：If-Match: "123456"
- 服务器会比对 If-Match 的字段值和资源的实体标记值（ETag），仅当两者一致时，才会执行请求。不然返回412。
- If-Match: *，这种情况直接忽略ETag的值。

7、If-None-Match
- 服务器会比对 If-None-Match 的字段值和资源的实体标记值（ETag），仅当两者不一致时，才会执行请求。

8、If-Modified-Since，格式：If-Modified-Since: Thu, 15 Apr 2004 00:00:00 GMT
- If-Modified-Since 字段值晚于Last-Modified，则希望服务器能处理该请求。
- If-Modified-Since 字段值早于Last-Modified，则返回304.

9、Referer，格式：Referer: http://www.hackr.jp/index.htm
- 告知服务器请求的原始资源的 URI。

10、User-Agent，格式：User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:13.0) Gec
- 会将创建请求的浏览器和用户代理名称等信息传达给服务器。

### 响应首部字段：从服务器端向客户端返回响应报文时使用的首部。
<div>
    <img src="./images/http_responseHeader.png">
</div>

### 实体首部字段：针对请求报文和响应报文的实体部分使用的首部
<div>
    <img src="./images/http_entityHeader.png">
</div>


## 常用内容编码
- gzip（GNU zip）
- compress（UNIX 系统的标准压缩）
- deflate（zlib）
- identity（不进行编码）

## HTTP状态码
<div>
    <img src="./images/http_statusCode.png">
</div>

- 2XX
```
    1、200 OK    表示从客户端发来的请求在服务器端被正常处理了。
    2、204 No Content    该状态码代表服务器接收的请求已成功处理，但在返回的响应报文中不含实体的主体部分，
                         也不允许返回任何实体的主体。
    3、206 Partial Content   该状态码表示客户端进行了范围请求，而服务器成功执行了这部分的GET 请求。
                             响应报文中包含由 Content-Range 指定范围的实体内容 
```
- 3XX
```
    1、301 Moved Permanently    永久性重定向。该状态码表示请求的资源已被分配了新的 URI，以后应使用资源现在所指的 URI。
    2、302 Found   临时性重定向。该状态码表示请求的资源已被分配了新的 URI，希望用户（本次）能使用新的 URI 访问。
    3、303 See Other    该状态码表示由于请求对应的资源存在着另一个 URI，应使用 GET方法定向获取请求的资源。
    4、304 Not Modified    该状态码表示客户端发送附带条件的请求（ GET 方法的请求报文中包含 If-Match，If-Modified-Since，
                           If-None-Match，If-Range，If-Unmodified-Since 中任一首部。） 时，服务器端允许请求访问资源，
                           但未满足条件的情况。即缓存文件仍未过时，可以使用缓存文件
    5、307 Temporary Redirect    临时重定向。该状态码与 302 Found 有着相同的含义。
```
**注意： 303 状态码和 302 Found 状态码有着相同的功能，303 状态码明确表示客户端应当采用 GET 方法获取资源，这点与 302 状态码有区别。**

- 4XX
```
    1、400 Bad Request    该状态码表示请求报文中存在语法错误。 
    2、401 Unauthorized    该状态码表示发送的请求需要有通过 HTTP 认证（BASIC 认证、DIGEST 认证）的认证信息。
                           另外若之前已进行过 1 次请求，则表示用户认证失败。
    3、403 Forbidden    该状态码表明对请求资源的访问被服务器拒绝了。
    4、404 Not Found    该状态码表明服务器上无法找到请求的资源。
```

- 5XX
```
    1、500 Internal Server Error    该状态码表明服务器端在执行请求时发生了错误。
    2、503 Service Unavailable    该状态码表明服务器暂时处于超负载或正在进行停机维护，现在无法处理请求。
```

## 通信数据转发程序
- 代理：代理是一种有转发功能的应用程序。代理服务器的基本行为就是接收客户端发送的请求后转发给其他服务器。代理不改变请求 URI，会直接发送给前方持有资源的目标服务器。
```
    代理的的作用：
        1、利用缓存技术减少网络带宽的流量
        2、组织内部针对特定网站的访问控制
        3、以获取访问日志为主要目的
    代理的分类：
        1、缓存代理：代理转发响应时，缓存代理（Caching Proxy）会预先将资源的副本（缓存）保存在代理服务器上。
        2、透明代理：转发请求或响应时，不对报文做任何加工的代理类型被称为透明代理
```
<div>
    <img src="./images/http_proxy.png">
</div>

- 网关：网关是转发其他服务器通信数据的服务器。
```
    网关能使通信线路上的服务器提供非 HTTP 协议服务。
```
<div>
    <img src="./images/http_gate.png">
</div>

- 隧道：隧道是在相隔甚远的客户端和服务器两者之间进行中转，并保持双方通信连接的应用程序。

```
    隧道可按要求建立起一条与其他服务器的通信线路，届时使用 SSL 等加密手段进行通信。
    隧道的目的是确保客户端能与服务器进行安全的通信。
    隧道本身不会去解析 HTTP 请求。
```


