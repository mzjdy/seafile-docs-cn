# 安全机制

## 客户端和服务器间的通信加密

Seafile 在服务器配置了 HTTPS 后，客户端会自动使用 HTTPS 协议和服务器通信。

## 加密资料库如何工作？

当你创建一个加密资料库，你将为其提供一个密码。所有资料库中的数据在上传到服务器之前都将用密码进行加密。

加密流程：

1. 生成一个32字节长的加密的强随机数。它将被用作文件加密秘钥（“文件秘钥”）。

2. 用用户提供的密码对文件秘钥进行加密 (使用PBKDF2算法)。加密后的文件秘钥将会被发送到服务器并保存下来。

3. 在文件同步的时候，先用用户输入的密码解密出文件秘钥，然后使用文件秘钥加密文件(使用AES 256/CBC 算法)，加密完后再上传文件。下载的时候，先用用户输入的密码解密出文件秘钥，然后使用文件秘钥解密文件。在上述过程中，你的密码将不会被传输到服务器上。


> 客户端加密目前并不支持云端文件浏览器, 当你使用云端文件浏览器加密、解密资料库时，密码会被传输到服务器上，并在服务器上保存一个小时。
