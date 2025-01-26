## ssh配置记录

##### 1.检查以前是否配置

`cd ~/.ssh`  

切换到ssh 根目录 寻找 ssh文件

![屏幕截图 2025-01-19 193443](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120130921047.png)

图示即是没有配置过，继续下一步；

##### 2. 本地设置生成ssh

![屏幕截图 2025-01-19 194022](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120132012465.png)

默认一路 回车 到底即可；

##### 3. 获取ssh公钥内容

`cd ~/.ssh`            寻找

`cat id_rsa.pub`  查看

![屏幕截图 2025-01-19 194421](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120132041789.png)

##### 4. 复制公钥进行远程仓库github上的添加

![屏幕截图 2025-01-19 194644](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133054602.png)

​	新建ssh之后,把刚刚的公钥复制进去保存即可

![屏幕截图 2025-01-19 194846](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133106851.png)

##### 5. 本地验证是否设置成功

`ssh -T git@github.com`

![屏幕截图 2025-01-19 195308](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133120513.png)

出现类似上图提示即为设置成功

##### 6. 出现的问题一：

在进行本地验证时，出现下图错误的信息

![屏幕截图 2025-01-19 195508](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133132024.png)

这里给出解决办法之一：

1. 在刚刚的~/.ssh 目录 下新增配置文件

2. `vim config`

3. 添加以下配置

4. ```bat
   Host github.com
   User xxx@xxx.com (ps:your email)
   Hostname ssh.github.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/id_rsa
   Port 443
   ```

如下图所示：

![屏幕截图 2025-01-19 200108](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133205193.png)

然后在进行验证即可成功！

##### 7. 关于使用ssh的原理

本地保存私钥，公钥放在远程仓库；

一次登录过程：

本地向远程发起登录请求，远程收到后随机生成一个字符串用公钥加密并发送回本地；

本地拿到后用私钥进行解密再次发送到远程，远程对比该解密后的字符串与源字符串是否相同；

相同则匹配成功。

**ssh 的配置是针对每台主机的！！！**

##### 8. 一次推送过程测试

![屏幕截图 2025-01-19 202452](https://gitee.com/jak-ma/graph-s/raw/master/imgs/20250120133222902.png)

​	