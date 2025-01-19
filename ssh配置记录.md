## ssh配置记录

##### 1.检查以前是否配置

`cd ~/.ssh`  

切换到ssh 根目录 寻找 ssh文件

![image-20250119193445564](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119193445564.png)

图示即是没有配置过，继续下一步；

##### 2. 本地设置生成ssh

`ssh-keygen -t rsa -C "email@xxx.com"` 

![image-20250119194025581](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119194025581.png)

默认一路 回车 到底即可；

##### 3. 获取ssh公钥内容

`cd ~/.ssh`            寻找

`cat id_rsa.pub`  查看

![image-20250119194423517](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119194423517.png)

##### 4. 复制公钥进行远程仓库github上的添加

![image-20250119194731494](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119194731494.png)

​	新建ssh之后,把刚刚的公钥复制进去保存即可	![image-20250119194850254](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119194850254.png)

##### 5. 本地验证是否设置成功

`ssh -T git@github.com`

![image-20250119195310926](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119195310926.png)

出现类似上图提示即为设置成功

##### 6. 出现的问题一：

在进行本地验证时，出现下图错误的信息

![image-20250119195511204](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119195511204.png)

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

![image-20250119200111064](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119200111064.png)

然后在进行验证即可成功！

##### 7. 关于使用ssh的原理

本地保存私钥，公钥放在远程仓库；

一次登录过程：

本地向远程发起登录请求，远程收到后随机生成一个字符串用公钥加密并发送回本地；

本地拿到后用私钥进行解密再次发送到远程，远程对比该解密后的字符串与源字符串是否相同；

相同则匹配成功。

**ssh 的配置是针对每台主机的！！！**

##### 8. 一次推送过程测试

![image-20250119202456914](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119202456914.png)

![image-20250119202549807](C:\Users\jakma\AppData\Roaming\Typora\typora-user-images\image-20250119202549807.png)

​	