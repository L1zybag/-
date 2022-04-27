#### 一.测试基础

**（软件测试是控制软件质量的重要手段和关键活动）**

<img src="/Users/mac/Library/Application Support/typora-user-images/image-20220419233757791.png" alt="image-20220419233757791" style="zoom: 33%;" />

**没有发现错误的测试也是有价值的，软件质量的一种方法）**

##### 	1.测试方法

​		（p1 概述部分软件测试方法分为白盒测试和黑盒测试）

###### 		1.白盒测试方法：

​			1.动态测试方法：

​				逻辑覆盖法p4:根据**覆盖的标准（选择题，填空题）**不同，分为**语句覆盖、判定覆盖、条件覆盖、条件判定覆盖**等。

​				路径分析法 ：又称为控制流覆盖，是一种按照程序内部逻辑结构和编码结构设计测试用例的测试方法。

​			2.静态测试方法：在不执行的条件下有条理地仔细审查软件设计、体系结构和代码，从而找出软件缺陷的过程，有时				也称为结构分析。

###### 		2.黑盒测试方法：

​		**等价类划分法、边界值分析法、决策表、因果图**等	

##### 	2.软件测试的目的以及好处：

​	目的：是为了验证产品是否完成了必要的功能 
​	好处：降低开发成本、提高性能以及防止错误



#### 二.自动化测试

###### 	1.手工测试的局限性p18

​	<img src="/Users/mac/Library/Application Support/typora-user-images/image-20220419234000406.png" alt="image-20220419234000406" style="zoom:33%;" />

###### 	2.分层自动化测试： p19上面三角图

​			上层用户界面（UI层）、中层接口测试、底层单元测试

<img src="/Users/mac/Library/Application Support/typora-user-images/image-20220419234328259.png" alt="image-20220419234328259" style="zoom: 25%;" />

###### 	3.自动化测试的详细分类（P19 ）：

​		（填空题）界面测试、单元测试、安全测试、数据库测试、负载测试、压力测试、可靠性测试

<img src="/Users/mac/Library/Application Support/typora-user-images/image-20220419234407854.png" alt="image-20220419234407854" style="zoom:25%;" />

###### 	4.自动化测试适合场景:（百度，还有看看习题）

​		1、需求稳定，不会频繁变更。
​		2、研发和测试周期长，需要频繁进行回归测试。
​		3、需要在多种平台上重复运行相同的测试场景。
​		4、某些测试项目通过手工测试无法实现或实现成本过高。
​		5、被测软件的开发过程较为规范，能够保证测试行



#### 三.unittest p55

###### 	1.核心概念（组成部分）：

​	**test case**:一个TestCase的实例就是一个测试用例，包括完整的测试流程，如测试前准备环境的搭建(setup)，执行(run)测试代码，以及测试后环境的还原(teardown)

​	**test suite**:多个testcase集合在一起，就是测试套件（testsuite）test suite可以嵌套test suite

​	**test loader**:加载testcase到test suite中，其中loadTestsFrom__()方法用于寻找test case，并创建他们的实例，然后添加到test suite中，返回test suite实例

​	**test runner**:用于执行测试用例，负责对整个测试过程进行跟踪。

###### 	2.断言方法p57：记一下方法名称，可能会写编程题，记前面两个 

​			assertIsNot、assertNotEqual

<img src="/Users/mac/Library/Application Support/typora-user-images/image-20220419235220956.png" alt="image-20220419235220956" style="zoom: 33%;" />	

##### 	3.源代码：对百度做访问测试  （编写测试用例setup、testxxx、teatDown）

​	请求，返回状态码，返回体什么什么的

```python
import gzip
import unittest
import requests
import urllib.request
from bs4 import BeautifulSoup
# -*- coding: utf-8 -*-
class Test(unittest.TestCase):
    def setUp(self):
        self.url="https://www.baidu.com/"
        self.headers={
            "User-Agent": 
            "Accept": 
            "Host": 
            "Referer": 
        }
        pass

    def test(self):
        response=requests.get(url=self.url,headers=self.headers)
        
        self.assertEqual(200,response.status_code)
        
        page_content=response.content.decode(response.encoding)
        
        page_content=BeautifulSoup(page_content,"html.parser")
        
        data_list=page_content.find_all("script")
        for item in data_list:
            print(item)
        pass

    def tearDown(self):
        pass
```

#### 四.selenium

##### 1.源代码：51job 前程无忧城市工作岗位测试=》输出html页面结果（就是.text）

```python
import time
from selenium import webdriver
from selenium.webdriver.common.by import By

def driver():
    url = "https://www.51job.com/(会换个别的网站)"
    driver = webdriver.Chrome("题目中给出的路径")
    driver.get(url)
    city_list = driver.find_elements(By.XPATH, "//div[@class='hcity']/div[@class='li']/a")
    for i in city_list:
        if i.text == '武汉':
            i.click()
    # 重新请求到新的网址
    driver.switch_to.window(driver.window_handles[-1])  # 切换到新的窗口
    driver.find_element(By.XPATH, "//div[@class='fbox']/div[1]/button[1]").click()
    job_info = driver.find_element(By.XPATH, "//div[@class='j_joblist']").text
    print(job_info)
if __name__ == '__main__':
    driver()

```

##### 2.p3 定位网页元素：find_elelment_by* id/name/className/tagName （6)



##### 3.什么是xpath? (简答题)

- XPath 使用路径表达式在 XML 文档中进行导航
- XPath 包含一个标准函数库
- XPath 是 XSLT 中的主要元素
- XPath 是一个 W3C 标准



##### 4.负载测试和压力测试：

###### 	**1.异同点：（必考）相同都是加压加载，不同是 负载测试是在高压情况下看表现情况，压力测试是测试最大负载额度**

###### 	**2.负载测试的加压方式：**

​		**一次加载**:一次性加载某个数量的用户，在预定的时间段内持续运行。

​		**递增加载**：有规律地增加用户，每几秒增加一些新用户，交错上升。

​		**高低突变加载**：某个时间用户数量很大，突然降到很低，过一段时间，又突然加到很高，反复几次。

​		**随机加载方式**：由随机算法自动生成某个数量范围内变化的、动态的负载，这种方式可能是和实际情况最接近的一种负									载方式

###### 	3.压力测试的分类p22：

​		**稳定性压力测试**：在选定的压力值下，持续运行24小时以上的测试。

​		**破坏性压力测试**：通过破坏性不断加压的手段，往往能快速造成系统崩溃或让问题明显地暴露出来。

###### 	4.渗透测试的基本流程：（百度一下）

![img](https://img-blog.csdnimg.cn/img_convert/5b24c1c0ca34d63bcfe8a8c892500bdb.webp?x-oss-process=image/format,png)

(1 )明确目标

当测试人员拿到需要做渗透测试的项目时，首先确定测试需求，如测试是针对业务逻辑漏洞，还是针对人员管理权限漏洞等;然后确定客户要求渗透测试的范围，如IP段、域名、整站渗透或者部分模块渗透等;最后确定渗透测试规则，如能够渗透到什么程度，是确定漏洞为止还是继续利用漏洞进行更进一步的测试，是否允许破坏数据，是否能够提升权限等。 在这一阶段，测试人员主要是对测试项目有一个整体明确的了解，方便测试计划的制订。

(2)收集信息

在信息收集阶段要尽量收集关于项目软件的各种信息。例如，对于一个Web应用程序，要收集脚本类型、服务器类型、数据库类型以及项目所用到的框架、开源软件等。信息收集对于渗透测试来说非常重要，只有掌握目标程序足够多的信息，才能更好地进行漏洞检测。

信息收集的方式可分为以下2种。

①主动收集：通过直接访问、扫描网站等方式收集想要的信息，这种方式可以收集的信 息比较多，但是访问者的操作行为会被目标主机记录。

②被动收集：利用第三方服务对 目标进行了解，如上网搜索相关信息。 这种方式获取的 信息相对较少且不够直接，但目标主机不会发现测试人员的行为。

(3)扫描漏洞

在这一阶段，综合分析收集到的信息，借助扫描工具对目标程序进行扫描，查找存在的安全漏洞。

(4)验证漏洞

在扫描漏洞阶段，测试人员会得到很多关于目标程序的安全漏洞，但这些漏洞有误报，需要测试人员结合实际情况，搭建模拟测试环境对这些安全漏洞进行验证。被确认的安全漏洞才能被利用执行攻击。

(5)分析信息

经过验证的安全漏洞就可以被利用起来向目标程序发起攻击，但是不同的安全漏洞，攻击机制并不相同，针对不同的安全漏洞需要进一步分析，包括安全漏洞原理、可利用的工具、目标程序检测机制、攻击是否可以绕过防火墙等，制订一个详细精密的攻击计划，这样才能保证测试顺利执行。

(6)渗透攻击

渗透攻击就是对目标程序发起真正的攻击，达到测试目的，如获取用户账号密码、截取目标程序传输的数据、控制目标主机等。一般渗透测试是一次性测试，攻击完成之后要执行清理工作，删除系统日志、程序日志等，擦除进人系统的痕迹。

(7)整理信息

渗透攻击完成之后，整理攻击所获得的信息，为后面编写测试报告提供依据。

(8)编写测试报告

测试完成之后要编写测试报告，阐述项目安全测试目标、信息收集方式、漏洞扫描工具以及漏洞情况、攻击计划、实际攻击结果、测试过程中遇到的问题等。此外，还要对目标程序存在的漏洞进行分析，提供安全有效的解决办法。





#### 	五.pylot的命令（主） ；ab命令 （6分编程题） 

​			pylot加压，直接打印出最终的测试结果，web压力测试非常方便

​		(考试考这三步 写命令)

​		第一步：修改配置文件（把测试的网址写入）

​		第二步：执行命令：python run.py -a 1000 -d 4 //a，并发台数，d,访问多少秒 1000个请求并发访问，访问4秒

​		第三步：输出结果

​		apachebench：加压，不属于python，是java

​		一个命令：ab -c 10 -n -100 https://www.baidu.com/

#### 	六.安全测试登录p20 

​	安全测试采用**建立整体的威胁模型、测试溢出漏洞、信息泄漏、错误处理、SQL注入、身份验证和授权错误、XSS攻击。**

##### 		1.安全测试途径(可能是我写的也可以是上面的采用的模型)：

​			**①尝试截取、破译、获取系统密码**

​			**②让系统失效、瘫痪、将系统制服，是其他人无法访问，自己非法进入**

##### 		2.安全测试的工具：**NMAP和Acunetix**

##### 		3.登录爆破 无限登录（百度）、 注入式攻击（百度）（9分）





#### /////课上复习的/////

系统：（填空题）

安全测试：

压力测试/负载测试

  途径是一致：加压（增加系统的访问量已经并发量）

一次加载、递增加载、高低突变加载、随机加载

目标不一样：

压力测试是想得到峰值（访问量最大、并发量最大）

负载测试是想得到压力大的情况下，反应的速度（响应时间是多少、事务处理速度怎么样，一般得到时间相关的值）

python：http://www.pylot.org/

pylot加压，直接打印出最终的测试结果，web压力测试非常方便

(考试靠着三步 写命令)

第一步：修改配置文件（把测试的网址写入）

第二步：执行命令：python run.py -a 1000 -d 4 //a，并发台数，d,访问多少秒 1000个请求并发访问，访问4秒

第三步：输出结果

apachebench：加压，不属于python，是java

一个命令：ab -c 10 -n -100 https://www.baidu.com/



