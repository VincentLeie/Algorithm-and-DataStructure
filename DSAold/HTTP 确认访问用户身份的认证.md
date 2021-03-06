#### 一.认证

1.密码:只有本人才会知道的字符串信息

2.动态令牌:仅限本人持有的设备内显示的一次性密码

3.数字证书:仅限本人(终端)持有的信息

4.生物认证:指纹和虹膜等本人的生理信息

5.IC卡等:仅限本人持有的信息

认证方式:

(1)BASIC认证(基本认证)

(2)DIGSET(摘要认证)

(3)SSL客户端认证

(4)FromBase认证(基于表单认证)

##### 1.basic认证

http/1.0就已经定义的认证方式

(1)返回状态码401以告知客户端需要进行认证

(2)用户ID和密码以Base64方式编码后发送

(3)认证成功者返回状态码200，若认证失败则返回状态码401

##### 2.digest认证 摘要认证

(1)发送临时的质询码(随机数，nonce)以及告知需要认证的状态码401

(2)发送摘要以及由质询码计算出的响应码

(3)认证成功返回状态码200，失败则再次发送状态码401

##### 3.SSL客户端认证

(1)接收到需要认证资源的请求，服务器会发送Certificate Request 报文，要求客户端提供客户端证书。

(2)用户选择将发送的客户端证书后，客户端会把客户端证书信息以Client Certificate报文方式发送给服务器

(3)服务器验证客户端证书验证通过后方可领取证书内客户端的公开密钥，然后开始HTTPS加密通信。

SSL认证采用双因素认证，不会仅依靠证书完成认证，一般会和基于表单认证组合形成一种双因素认证来使用

第一个认证因素的SSL客户端证书用来认证客户端计算机，另一个因素的密码则用来确定这是用户本人行为的。

SSL认证需要一定的费用

##### 4.基于表单的认证

认证多半为基于表单的认证，由于使用上的便利性及安全性的问题，HTTP协议标准提供的basic认证和digest认证几乎不怎么使用。另外，SSL客户端认证虽然具有高度的安全等级，但因为导入及维持费用问题，还尚未普及。

Session管理及Cookie应用

鉴于HTTP是无状态协议，之前已经认证成功的用户状态无法通过协议层面保存下来，无法实现状态管理，因此即使当该用户下一次继续访问，也无法区分他与其他的用户。于是我们用Cookie来管理Session，以弥补HTTP协议中不存在的状态管理功能。

(1)发送已登录信息(用户ID，密码)

(2)服务器会发放包含Session ID的Cookie

(3)客户端接收到从服务器端发来的Session ID后，会将其作为Cookie保存在本地。下次向服务器发送请求时，浏览器会自动发送Cookie，所以Session ID也随之发送到服务器。



