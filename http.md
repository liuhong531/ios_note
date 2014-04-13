一．HTTP请求

1．HTTP请求格式：

<request line>

<headers>

<blank line>

[<request-body>]

在HTTP请求中，第一行必须是一个请求行（request line），用来说明请求类型、要访问的

资源
以及使用的HTTP版本。紧接着是一个首部（header）小节，用来说明服务器要使用的附加信息。在首部之后是一个空行，再此之后可以添加任意的其他数据[称之为主体（body）]。
2．GET与POST区别

HTTP 定义了与服务器交互的不同方法，最基本的方法是 GET 和 POST（Ajax

开发
，关心的只有GET请求和POST请求）。
GET与POST方法有以下区别：

（1）   在客户端，Get方式在通过URL提交数据，数据在URL中可以看到；POST方式，数据放置在HTML HEADER内提交。

（2）   GET方式提交的数据最多只能有1024字节，而POST则没有此限制。

（3）   安全性问题。正如在（1）中提到，使用 Get 的时候，参数会显示在地址栏上，而 Post 不会。所以，如果这些数据是中文数据而且是非敏感数据，那么使用 get；如果用户输入的数据不是中文字符而且包含敏感数据，那么还是使用 post为好。

（4）   安全的和幂等的。所谓安全的意味着该操作用于获取信息而非修改信息。幂等的意味着对同一 URL 的多个请求应该返回同样的结果。完整的定义并不像看起来那样严格。换句话说，GET 请求一般不应产生副作用。从根本上讲，其目标是当用户打开一个链接时，她可以确信从自身的角度来看没有改变资源。比如，新闻站点的头版不断更新。虽然第二次请求会返回不同的一批新闻，该操作仍然被认为是安全的和幂等的，因为它总是返回当前的新闻。反之亦然。POST 请求就不那么轻松了。POST 表示可能改变服务器上的资源的请求。仍然以新闻站点为例，读者对文章的注解应该通过 POST 请求实现，因为在注解提交之后站点已经不同了（比方说文章下面出现一条注解）。
http://www.cnblogs.com/stu-acer/archive/2006/08/28/488802.html

 GET与POST方法实例：


GET实例	POST实例
GET /books/?name=Professional%20Ajax HTTP/1.1

Host: www.wrox.com

User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)

Gecko/20050225 Firefox/1.0.1

Connection: Keep-Alive










 
POST / 

HTTP
/1.1
Host: www.wrox.com

User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)

Gecko/20050225 Firefox/1.0.1

Content-Type: application/x-www-form-urlencoded

Content-Length: 40

Connection: Keep-Alive

     （此处空一行）

name=Professional%20Ajax&publisher=Wiley




 

       3．表单提交中get和post方式的区别归纳如下几点：

（1）get是从服务器上获取数据，post是向服务器传送数据。

（2）对于表单的提交方式，在服务器端只能用Request.QueryString来获取Get方式提交来的数据，用Post方式提交的数据只能用Request.Form来获取。

（3）一般来说，尽量避免使用Get方式提交表单，因为有可能会导致安全问题。比如说在登陆表单中用Get方式，用户输入的用户名和密码将在地址栏中暴露无遗。但是在分页程序中，用Get方式就比用Post好。

二．HTTP响应

1．HTTP响应格式：

<status line>

<headers>

<blank line>

[<response-body>]

在响应中唯一真正的区别在于第一行中用状态

信息
代替了请求信息。状态行（status line）通过提供一个状态码来说明所请求的资源情况。 
       
       HTTP响应实例：

HTTP/1.1 200 OK

Date: Sat, 31 Dec 2005 23:59:59 GMT

Content-Type: text/html;charset=ISO-8859-1

Content-Length: 122

＜html＞

＜head＞

＜title＞Wrox Homepage＜/title＞

＜/head＞

＜body＞

＜!-- body goes here --＞

＜/body＞

＜/html＞

2．最常用的状态码有：

◆200 (OK): 找到了该资源，并且一切正常。

◆304 (NOT MODIFIED): 该资源在上次请求之后没有任何修改。这通常用于浏览器的缓存机制。

◆401 (UNAUTHORIZED): 

客户
端无权访问该资源。这通常会使得浏览器要求用户输入用户名和密码，以登录到服务器。
◆403 (FORBIDDEN): 客户端未能获得授权。这通常是在401之后输入了不正确的用户名或密码。

◆404 (NOT FOUND): 在指定的位置不存在所申请的

资源


http请求头：

Accept: text/html,image/*    浏览器通过这个头，告诉服务器它所支持的数据类型
Accept-Charset： 浏览器通过这个头，告诉服务器它采用的字符集
Accept-Encoding：浏览器通过这个头，告诉服务器，它所支持的压缩格式
Accept-Language：浏览器通过这个头，告诉服务器，它所采用的语言
Host：浏览器通过这个头，告诉服务器，我想访问服务器哪台主机
If-Modified-Since：浏览器通过这个头，告诉服务器，它缓存数据时间是多少。
Referer：浏览器通过这个头，告诉服务器，我是从哪个网页点过来的（防盗链）
User-Agent: 浏览器通过这个头，告诉服务器，当前浏览器操作系统的信息，以及浏览器的版本号
Connection：
Date: 



//prepar request
NSString *urlString = [NSString stringWithFormat:@"http://urlToSend.com"];
NSMutableURLRequest *request = [[[NSMutableURLRequest alloc] init] autorelease];
[request setURL:[NSURL URLWithString:urlString]];
[request setHTTPMethod:@"POST"];
 
//set headers
NSString *contentType = [NSString stringWithFormat:@"text/xml"];
[request addValue:contentType forHTTPHeaderField: @"Content-Type"];
 
//create the body
NSMutableData *postBody = [NSMutableData data];
[postBody appendData:[[NSString stringWithFormat:@"<xml>"]dataUsingEncoding:NSUTF8StringEncoding]];
[postBody appendData:[[NSString stringWithFormat:@"<yourcode/>"]dataUsingEncoding:NSUTF8StringEncoding]];
[postBody appendData:[[NSString stringWithFormat:@"</xml>"]dataUsingEncoding:NSUTF8StringEncoding]];
 
//post
[request setHTTPBody:postBody];
 
//get response
NSHTTPURLResponse* urlResponse = nil;
NSError *error = [[NSError alloc] init];
NSData *responseData = [NSURLConnection sendSynchronousRequest:request returningResponse:&urlResponse error:&error];
NSString *result = [[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding];
NSLog(@"Response Code: %d", [urlResponse statusCode]);
if ([urlResponse statusCode] >= 200 && [urlResponse statusCode] < 300) {
NSLog(@"Response: %@", result);
 
//here you get the response
 
}