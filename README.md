# bug_scan
fofa联动nuclei实现批量漏扫
#### 项目介绍
这是一个结合fofa和nuclei的批量漏洞扫描脚本，能够根据给出的关键词进行批量化扫描，
适合放在linux服务器上，24小时自动扫描

其中fofa查询部分调用了fofamap的项目,修改了部分代码：https://github.com/asaotomo/FofaMap

## 使用说明

把scan文件放到/root下，放好之后scan的目录是/root/scan

#### 环境配置

###### python3 ：

这个自行安装，我用的python3.8和3.11都能运行，其他应该也没啥问题

###### nuclei：

去官方下载nuclei，这里我只讲单文件版本配置方式，github的nuclei官方项目：[nuclei](https://github.com/projectdiscovery/nuclei)
进入release，选择适合自己的版本，这里我用的是amd64的，解压出来然后使用chmod u+x nuclei给予执行权限，然后mv nculei 环境变量目录，就可以直接使用了
![image.png](https://image.3001.net/images/20230527/1685165496_647195b85b31c3b3ee0a4.png!small)

###### 然后是fofamap的环境配置

我会放在requirements.txt内，大家下载好后进入requirements所在目录内执行命令即可安装依赖：
pip3 install -r requirements.txt
#### 使用步骤

###### 给予bug\_scan.sh执行权限

scan文件下载好放到/root文件下，进入/root/scan文件内，给予执行权限chmod u+x bug\_scan.sh

###### keyword.txt（搜索关键词文件）放到/root目录下

keyword内容为我们要搜索的语句的内容
keyword.txt内容格式为,与fofa查询语句格式一致：

```
title="xxx" && after="2022-1-6"
title="xxx" && after="2022-1-10"
```

###### 填写fofa配置(需要fofa会员)

我们将fofamap的配置文件fofa.ini中email和key填写（最好是旧高级会员账号的key），以及根据自己的需求填写其他配置内容即可，而logger一定要设置为on，因为我们就是从日志文件fofamap.log中提取扫描目标的。

###### 最后一步

执行/root/scan/bug.scan.sh文件，就会开始循环keyword.txt内搜索关键词进行扫描，最后输出结果放在/root/scan\_result内，cat /root/scan\_result即可
一开始scan_result是没东西的，要扫描出来才有，还有如果是服务器建议用screen跑，这样断开会话还能继续扫

## 声明
本工具仅提供给安全测试人员进行合法安全测试使用 用户滥用造成的一切后果与作者无关 使用者请务必遵守当地法律 本程序不得用于商业用途，仅限学习交流

## 题外话
有啥问题欢迎各位提出，第一次用github上传，请大佬们多多担待
关键词搜的好，cnvd证书也不在话下

最近建了一个交流群，旨在提供一个师傅们可以交流、讨论技术以及分享信息的平台（别灌太多水），加群有门槛（满足CNVD证书、众测提交过一定数量漏洞等任一要求），感兴趣的可以加我的微信
![image](https://github.com/some-new-codes/bug_scan/assets/76439220/ef41978b-bc8e-4c95-af88-5c5ba70b912e)
