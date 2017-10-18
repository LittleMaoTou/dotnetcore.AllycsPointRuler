# dotnetcore.AllycsPointRuler
配置xml的通用积分规则计算系统支持.netcore（推荐部署为docker）
目前通过规则的编排可以完成99%的积分需求。
如有问题联系作者allycs@126.com

-----------------------------------------------------码农不需要，割了-----------------------------------------------------

# 源码结构
> 方法主体（类库支持.netcore）：
>> AllycsPointRuler

> 项目样例：
>> DemoNancyDotnetCore（nancy的简单样例）

# xml配置参考（源码根目录BaseRuler.xml）

```
<?xml version="1.0" encoding="UTF-8"?>
<ROOT>
  <BASE_IN>
    <BASE>
      <ISONLY>FALSE</ISONLY>
      <WEIGHT>0</WEIGHT>
      <AMOUNT>20</AMOUNT>
      <POINT>1</POINT>
      <MULTIPLE>1</MULTIPLE>
      <PLUSORMINUS>TRUE</PLUSORMINUS>
    </BASE>
    <WEEK_2>
      <ISONLY>FALSE</ISONLY>
      <WEIGHT>0</WEIGHT>
      <AMOUNT>0</AMOUNT>
      <POINT>0</POINT>
      <MULTIPLE>2</MULTIPLE>
      <PLUSORMINUS>TRUE</PLUSORMINUS>
    </WEEK_2>
    <WEEK_5>
      <ISONLY>FALSE</ISONLY>
      <WEIGHT>0</WEIGHT>
      <AMOUNT>0</AMOUNT>
      <POINT>0</POINT>
      <MULTIPLE>3</MULTIPLE>
      <PLUSORMINUS>TRUE</PLUSORMINUS>
    </WEEK_5>
  </BASE_IN>
  <BASE_OUT>
    <BASE>
      <ISONLY>FALSE</ISONLY>
      <WEIGHT>0</WEIGHT>
      <AMOUNT>10</AMOUNT>
      <POINT>100</POINT>
      <MULTIPLE>1</MULTIPLE>
      <PLUSORMINUS>FALSE</PLUSORMINUS>
      <DEDUCTION>FALSE</DEDUCTION>
    </BASE>
  </BASE_OUT>
  <REG_IN>
    <BASE>
      <ISONLY>FALSE</ISONLY>
      <WEIGHT>0</WEIGHT>
      <AMOUNT>0</AMOUNT>
      <POINT>50</POINT>
      <MULTIPLE>1</MULTIPLE>
      <PLUSORMINUS>TRUE</PLUSORMINUS>
    </BASE>
  </REG_IN>
</ROOT>
```
# XML规则编写规范
> 根节点为`<ROOT>`

> `<BASE_IN>`、`<BASE_OUT>`节点为可配置项,BASE为自定义名称根据需要指定，“_IN”为固定格式代表产生积分，“_OUT”为固定格式为消费积分
  可根据需求配置多个，例如上例xml中就配置了注册产生积分“REG_IN”
  
> 具体的规则配置见下代码块
```
----以下为规则配置：可单个、多个（后追加"_0"、"_1"...）;例：<YEAE_2017_0>...</YEAE_2017_0>
----规则中的时间均已2位计,例如9月请写09；每个规则名称有且仅有一个，多个请名称后追加"_n"区分
BASE        ----基础规则（例：<BASE>...</BASE>）
YEAR        ----年（例：<YEAR_2017>...</YEAR_2017>）
MONTH       ----月（例：<MONTH_09>...</MONTH_09>) 
DAY         ----日（例：<DAY_31>...</DAY_31>)
WEEK        ----周几（例：<WEEK_2>...</WEEK_2>)周日为：0（一周从周日开始。0，1，2，3，4，5，6）
HOUR        ----小时（例：<HOUR_09>...</HOUR_09>)24小时制；每当时针到9时
MINUTE      ----分钟（例：<MINUTE_09>...</MINUTE_09>)每当分针到第9分钟
SECOND      ----秒钟（例：<SECOND_09>...</SECOND_09>)每当秒针到第9秒
YMD         ----年月日（例：<YMD_20170909>...</YMD_20171018>)2017年9月9日
MD          ----月日（例：<MD_0909>...</MD_0909>)9月9日
CHINESEMD   ----农历月日（例：<CHINESEMD_九月二十一>...</CHINESEMD_九月二十一>）详细格式参考ChineseDate类
MIWEEKS     ----某月的第几个星期几（例：<MIWEEKS_060300>...</MIWEEKS_060300>）该日期为父亲节
EVENT       ----类似基础规则（用来定义特定的活动或者规则多个请名称后追加"_n"区分）
```
# 可提供的功能
. 支持基础的
