# 运维平台部署过程与常见问题汇总

## 一、部署过程

## 二、常见问题
### 1、实时日志显示404 page not found
* 问题：<br><br>
![image](https://user-images.githubusercontent.com/27944125/220240070-5455f384-e0fb-4c3b-a2a3-451664baa5f0.png)

* 处理方法：<br><br>
  1、 在**主控节点**的hosts文件中添加受控节点：例如
  ```
  192.168.0.213 gzldxyy_onepay
  192.168.0.214 gzldxyy_yyds_db
  ```
  2、保证**主控节点**可以telnet通 *受控节点* 的 **7109** 端口<br><br>
  ![image](https://user-images.githubusercontent.com/27944125/220260513-cf585573-7dd1-48b7-8ee9-f3bd725b727f.png)
  <br><br>
  如果不通，请检查 **防火墙** 与 **tailon** 服务状态<br>

### 2、无法传输文件
* 问题：<br><br>
  点击产品或者应用部署的时候，一直显示传输文件大小，需要多少分钟<br>
  查询 **filepusher info日志**  没有刷POST传文件日志  <br>
  
* 处理方法：<br><br>
  1、检查 v1.5安装包是否执行
    ```
    windows: update.bat up
    linux: update.sh up 
    ```
  ![image](https://user-images.githubusercontent.com/27944125/220278691-bb091853-0db8-4f2b-bd36-1b1bab360293.png) <br><br>

  2、 检查是否配置了文件<br><br>
    在中心化运维平台中的 **主控节点** 的 **文件服务** 是否配置
    >默认的 x-upstream 地址前置多了一个 */* 斜杠，需要去掉，然后点保存 <br>


    ![image](https://user-images.githubusercontent.com/27944125/220286151-9f0c2496-70bc-45d4-890a-e3364ddf08de.png)


  3、检查 **前置服务器 webserver的ops配置** 是否正确配置
    ```
    根据实际安全路径进行调整
    windows: D:\\apps\app\webserver\conf\location\ops.conf 
    linux: /apps/app/webserver/conf/location/ops.conf
    ```
    把图中的方框部分删除，保留第一个 *location /ops/*  即可（需要重启前置的webserver）<br><br>
    ![image](https://user-images.githubusercontent.com/27944125/220280688-4a25bbfa-b7cd-4071-8d31-9c63abc1575a.png)

  
