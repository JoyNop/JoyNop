谷歌浏览器 Chrome+ShadowSocks(SS)+Proxy SwitchyOmega 自动翻墻


准备工作

1、谷歌浏览器 Chrome 内核或者Firefox

2、Shadowsocks  

3、谷歌浏览器Chrome代理插件 SwitchyOmega 2.5.20 for Chromium & Firefox，官方地址

小解释：

（Shadowsocks可以配合任意浏览器翻墙）

Chrome+ShadowSocks=能翻墙，可以自动判断部分常见被墻网站走代理，其他网站不走代理。

Chrome+ShadowSocks+Proxy SwitchyOmega=更智能的翻墙，除了上面的功能外还能自己自定义哪些网站走代理。

具体步骤

1、运行小飞机，并且确定填写了可以正常使用的密码信息。

2、安装Proxy SwitchyOmega扩展，正常来说运行了小飞机后就可以直接访问Chrome应用商店安装了。

3、对Proxy SwitchyOmega进行配置，如下图：



Proxy 配置

先跟着上面的图片填写好代理信息（特别提醒：小编近期发现这里要设置成http才能代理，如果你socks5代理不成功也试试http *问题所在），然后设置自动切换规则，如下图：

![1](/img/20190121095751.png)

Auto switch 配置

![1](/img/SwitchyOmega1.png)

点击auto switch后有一个添加在线规则的按钮，点击后就出现了上面图片中的界面，跟着填写即可，规则列表为：https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt（官方GFW地址，如果无法获取可使用下面地址）

![1](/img/SwitchyOmega2.png)

![1](/img/SwitchyOmega3.png)

国内无法访问可以使用这个额GFW规则地址：http://proxy.expand.ejcms.com/gfwlist.txt（每6个小时更新一次）

开启浏览器自动翻墙

然后最关键的一步，在浏览器右上角点击插件按钮，然后选择自动切换规则模式，这样只要在规则列表里面的网站都会翻墻访问。

对于没在翻墻规则里面的网站，可以自己添加规则（无法访问的时候插件那图标会有显示，点击后就可以看到快速添加方法。）