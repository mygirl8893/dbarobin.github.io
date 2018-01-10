---
layout: page
title: Blockchain
permalink: /blockchain/
---

***

**「区块链技术指北」**，常见价值虚拟货币的相关教程、区块链技术前沿信息、区块链技术好文品鉴和分享、区块链技术相关工具、区块链技术分析、区块链项目跟踪等。

> 如果对我感兴趣，想和我交流，我的微信号：**Wentasy**，加我时简单介绍下自己，并注明来自「区块链技术指北」。同时我会把你拉入微信群「区块链技术指北」。

#### Archive
***

<ul class="tags-box">
{% if site.posts != empty %}
    {% for tag in site.tags %}
        {% if tag[1].size > 1%}
            {% if tag[0] == 'Blockchain' %}
                {% for post in tag[1] %}
                    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time> &raquo;
                    <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a><br />
                {% endfor %}
            {% endif %}
        {% endif %}
    {% endfor %}
{% else %}
    <span>No posts</span>
{% endif %}
</ul>

#### Community
***

* [区块链技术指北，bcage.one](https://bcage.one)

#### GitHub
***

* [BlockchainAge](https://github.com/dbarobin/BlockchainAge)
* [mycrypto](https://github.com/dbarobin/mycrypto)

#### Referrals
***

* **币安**，[https://www.binance.com/?ref=11190872](https://www.binance.com/?ref=11190872)
* **OTCBTC** 是目前最流畅、最靠谱、最好用的场外交易平台，支持支付宝、微信、银行卡支付购买 BTC、ETH、EOS、USDT、QTUM、ZEC、GXS、BCH 等数字币。现在注册，即可领取比特币红包！ [https://otcbtc.com/referrals/ROBINWENIO](https://otcbtc.com/referrals/ROBINWENIO)
* **OKEx**，[https://www.okex.com/share/invite/3956Ew.do](https://www.okex.com/share/invite/3956Ew.do)
* **币乎**，[https://zt.bihu.com/?id=22207](https://zt.bihu.com/?id=22207)
* **BeeChat**，[https://in.ibeechat.com/spread/364159](https://in.ibeechat.com/spread/364159)
* **Mixin**，[https://mixin.one/enroll/369082](https://mixin.one/enroll/369082)
* **JEX**，[https://www.jex.com/user/register.do?utmSource=5404F3BC9D429B1D7AF](https://www.jex.com/user/register.do?utmSource=5404F3BC9D429B1D7AF)

#### Media
***

「区块链技术指北」同名 Telegram Channel：[https://t.me/BlockchainAge](https://t.me/BlockchainAge)，欢迎订阅。

同时，本系列文章会在以下渠道同步更新，欢迎关注：

* 「区块链技术指北」同名微信公众号（微信号：**BlockchainAge**）
* 「区块链技术指北」同名知识星球，**李笑来老师也加入了**，[https://t.xiaomiquan.com/ZRbmaU3](https://t.xiaomiquan.com/ZRbmaU3)
* 个人博客，[https://dbarobin.com](https://dbarobin.com)
* 知乎，[https://zhuanlan.zhihu.com/robinwen](https://zhuanlan.zhihu.com/robinwen)
* Steemit，[https://steemit.com/@robinwen](https://steemit.com/@robinwen)
* Medium，[https://medium.com/@robinwan](https://medium.com/@robinwan)

#### Donate
***

原创不易，读者可以通过如下途径打赏，虚拟货币、美元、法币均支持。

* **BTC**: 3QboL2k5HfKjKDrEYtQAKubWCjx9CX7i8f
* **ERC20 Token**: 0x8907B2ed72A1E2D283c04613536Fac4270C9F0b3
* **PayPal**: [https://www.paypal.me/robinwen](https://www.paypal.me/robinwen)

© Robin Wen