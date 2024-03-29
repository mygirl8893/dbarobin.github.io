---
published: true
author: Robin Wen
layout: post
title: 建站分享
category: 前端
summary: >-
  这次建站经历于我而言是相当宝贵的，很多看似简单的问题，真正实施的时候未必如此。常言知易行难，这次感触颇深。把整个建站过程分享给大家，希望能给读者丁点启示，实乃欣慰。更希望我在自己的小屋里好好写作，静心而为，大放异彩。
tags:
  - 前端
  - 建站
  - 博客
comments:
  - author:
      type: github
      displayName: dslztx
      url: 'https://github.com/dslztx'
      picture: 'https://avatars.githubusercontent.com/u/7435805?v=3&s=73'
    content: >-
      &#x4F60;&#x597D;&#xFF0C;&#x53EF;&#x4EE5;&#x9EBB;&#x70E6;&#x5E2E;&#x6211;&#x628A;&#x4E0A;&#x4E00;&#x6761;&#x6211;&#x7684;&#x8BC4;&#x8BBA;&#x5220;&#x6389;&#x5417;&#xFF0C;&#x66B4;&#x9732;&#x90AE;&#x7BB1;&#x5730;&#x5740;&#x6015;&#x6210;&#x4E3A;&#x5783;&#x573E;&#x90AE;&#x4EF6;&#x63A5;&#x6536;&#x8005;&#x4E86;
    date: 2016-06-26T03:53:47.271Z

---

## 目录 ##

* Table of Contents
{:toc}

`文/robin`

## 一 写在前面 ##

以前写过一篇文章，里面提到自己会建站，如今这个愿望在 2014 年之末 2015 年之初实现了。

热衷开源，热爱简单，已然成为我的标签。目前我的博客基于 `GitHub Pages`，主题使用 `So Simple Theme`，域名从`GoDaddy`申请，采用`DNSPod`解析域名，使用`安全宝`加速网站。本来打算使用七牛云存储或者又拍云缓存图片的，后来综合考虑，还是放弃了。只要有 Git 和 Vim 的地方我就能写博客，告别编辑框，告别枯燥无趣浪费时间的排版。

从 2011 年开始写博客，到目前已经跨过了好几个年头。CSDN 承载了太多回忆，解决一个问题的喜悦、收到别人赞赏的自豪、自我反思的进步……因为有了博客，才让我一步一步更加坚定地前行，才让我每天入睡前握紧拳头，才让我的目光注视着前方。感谢 CSDN ，让我的青春如此美好。

为什么要独立建站，一个是自己的原因，我不想受什么约束；另外一个是 CSDN 的体验，不想多言了，读者自行感受。

接下来我会把我的建站经历分享给大家。

## 二 选择 MarkDown ##

`MarkDown` 是一种非常简洁的网页标记语言，生于 HTML，高于 HTML。MarkDown 就是为简洁而生，HTML 写一大堆标签，MarkDown 用几个符号就可以很好的解决。接触 MarkDown 很早了，但真正广泛的使用还是在14年8月份左右。支持 MarkDown 的网站给我的印象非常好，比如 GitHub、简书、开源中国、博客园等等。以前写文章，在编辑框中插入文字后，还要花大量的时间折腾排版。使用 MarkDown，几个符号就可以完成很漂亮的排版，节省大量时间，从而让我更关注文字本身。所以，强烈推荐读者抛弃各类网站编辑器，各种文字编辑软件，一个 Vim，一个 Sublime，走遍天下都不怕。

## 三 选择 GitHub Pages ##

本来打算使用 VPS 搭建博客的，技术上于我而言不是难事。找过很多 VPS 供应商，比如国外的 Linode，Digital Ocean，国内的阿里云、百度云、新浪云，结果都不如意，要么是访问速度不够理想，要么是太贵。好吧，其实主要原因是太贵了，没钱就是这样，总想着怎么省钱。看过很多独立博客，很多都是基于 `GitHub Pages` 搭建的，然后去了解了下，发现这才是我的真爱啊。于是 Google 之，查了不少资料。GitHub Pages 针对个人用户提高免费的 300M 空间，也就是个人用户 Repo 的限制大小。300M 于我而言完全足够，因为图片我不打算放在 GitHub。GitHub Pages 基于 `Jekyll`，这是一个用 Ruby 写的静态博客系统，简洁，易于使用。多方思量后，敲定 GitHub Pages。

## 四 主题选择 ##

鉴于我的前端技术有限，没有自己开发主题。找了很多主题都不满意，要么太冗余，要么太丑。一次偶然，Google 链入到一个博客，令我眼前一亮，如此简洁，这不正是我喜欢的吗。在博客的 Footer，得知该主题是 `So Simple Theme`，由国外大牛 `Michael Rose`开发，自适应移动设备，这也省去了对移动端的优化了。找到 So Simple Theme 的主页，了解了下该主题的基本构成。使用该主题的步骤很简单，Fork、修改项目名、修改 Config，把文章放到 _post 目录，OK。当然，如果你想自定义一些功能，还得自行修改代码。

## 五 博客功能 ##

目前我的博客对外开放的功能有评论、分享、Feed 订阅、搜索，貌似就只有那么多。其他博客提供的功能在我看来基本无用。评论使用 `Disqus`，本来打算使用多说，但 UI 丑的掉渣，于是放弃了。Disqus 的使用非常简单，注册账号，添加网站，把 JS 代码添加到 GitHub Pages 中即可。

另外，我启用了 `Google Analytics`，登录到 `Google Analytics` 就可以很清晰的看到博客的访问情况，以及做一些分析。

## 六 博客同步 ##

利用空闲时间，我把 CSDN 和微信公众平台的部分文章同步到了 GitHub Pages 中。所有的文章重新排版，部分文章重新找图片。取其精华，去其糟粕，目前文章总数共一百来篇。博客的同步是相当耗时间的，往往调整一篇文章的格式就要花掉半个钟。业余时间除了看书，写文章，大部分时间都在同步博客。

## 七 域名申请 ##

域名提供商有很多，比如国外的 `GoDaddy` 、`Name` 等，国内有万网、时代互联等。多方了解后，还是决定在 GoDaddy 上注册域名，一是因为它是行业老大，服务、质量有保障；二是因为国内的这些域名提供商不是太靠谱；三是因为 GoDaddy 有很多优惠码可以使用；四是因为我不想备案自己的网站，就是一个博客而已，用不着。我注册的域名（dbarobin.com），两年，差不多 $19。GoDaddy 支持支付宝付款，但想到今后还要海淘很多东西，为什么不用自己的 VISA 信用卡呢？这样也可以增长些海淘的经验。使用信用卡付款遇到不少问题，比如直接使用信用卡支付不成功，老是提示我填写的信息有问题。无奈之下，只好使用 PayPal 了。我的 PayPal 关联了工银的 VISA 信用卡，很方便地就可以完成支付。现实就是这样，时不时会给你开个玩笑。成功拿下域名之后不久，我的 GoDaddy 账号就被封了。这种情况只好申诉，把我的 PayPal 支付详情、身份证正反面、信用卡正反面（信用卡图片最好处理好，把卡号打码）提供给 GoDaddy。在这个过程中，上传这些文件失败，尝试了数次之后，只好改发送邮件。但发送邮件却提示得不到回应，只好打客服。GoDaddy 的 Online Support 是一个美国的号码，拨通后，一连串的英文提示，我选择后，传来标准的美国式英语。我用基本流利的英语和他对话，提供了 Customer ID 和 PIN Number，叙述了我遇到的问题，他很耐心地为我解答。原来是我发送的邮件地址有问题，不应该发到 support@godaddy.com，而应该发到 verifypayment@godaddy.com。客服在24小时之内会给我反馈，其实等不了那么长时间，这个只是最慢的反馈速度，要相信老外的办事效率。反思我的账号为什么会被封，很可能是我的 GoDaddy 姓名和 PayPal 的姓名不一致。这次经历让我体会到英语的强大作用，后面还得继续巩固和加强英语，争取把我的口语练到 80 分。

## 八 域名绑定以及优化 ##

之前就从各种途径得知 `DNSPod` 是个神奇而伟大的网站，这次亲身体验才有这样的体验。针对个人用户，DNSPod 提供的服务已经足够使用。购买域名后，我在我的 GitHub Pages 里添加一个 CNAME 的文件，里面的内容很简单，就是我的域名。然后登录 DNSPod，添加域名，添加记录，我添加了三条，分别是两条 GitHub Pages 的 IP 地址、一条指向之前的 dbarobin.github.io，还有两条是 DNSPod 自动生成的 NameServer。接着登录 GoDaddy，在域名中把 NameServer 改成 DNSPod 提供的 NameServer。所有步骤完成后，等待数十分钟，访问 dbarobin.com，一个神奇的博客出现在你的眼前，如此闪亮，好似梦中的心爱姑娘，清澈明亮。

绑定完成后，在 `D 监控`中启用监控，自定义设置，之后就可以看到监控信息。如果网站不能访问，还可以根据你的设置给你发送邮件、短信或者微信提醒。特别是微信提醒这个功能，对于微信重度依赖者，实在是太赞了。D 监控设置完成后，可以在加速中心利用`安全宝`给你的网站加速。申请加速需要时间审核，审核通过后，会给你分配加速节点。由于我的网站没有备案，只给我分配了海外节点，不过 PING 域名基本上维持在 100 MS 左右，基本满意。另外，使用安全宝加速后，域名记录中，指向 GitHub Pages 中的 IP 被替换成安全宝分配的节点。

## 九 TroubleShooting ##

在建站的过程中，也遇到一些网站配置的问题，下面摘取部分，供读者参考。

### 9.1 返回到顶部按钮 ###

如果文章太长，拉到文章中部或者尾部的时候，想返回顶部，如果没有返回到顶部的按钮，只能通过滑动滚轮或者拉动滚动条，这是很糟的体验。于是我实现了返回到顶部的功能。要想实现这个功能，只需要准备一张有提示作用的图片，再添加 JS 代码即可解决。

### 9.2 修改字体 ###

So Simple Theme 默认提供的字体太大，于是我揣摩修改字体。但我怎么修改都不生效，只好在项目中 File a issue。根据作者的解答，原来是我使用的主题版本过低，修改 CSS 不再生效，而应该修改 SASS 文件。我修改了标题字体大小、正文字体大小，经过修改后，网站确实好看多了。

### 9.3 修改 BlockQuote 样式 ###

默认的 BlockQuote 样式很丑，看着很难受。于是我根据 GitHub 提供的默认 BlockQuote CSS 样式修改，比如修改成这样：

``` css
// Blockquotes
// --------------------------------------------------

blockquote {
    font-family: $alt-font;
    font-style: normal;
    @include font-size(11);
    padding-left: 15px;
    border-left: 4px solid #DDD;
    color: #777;
}
```

这样的效果比较满意，赞。

### 9.4 增加分享到 QQ 空间和微博 ###

默认可以分享到 Facebook、Twitter、Google +，这显示不符合国人口味。于是我添加了分享到 QQ 空间和微博的功能，只需要修改 `social-share.html` 文件，添加分享到 QQ 空间和微博的 URL 即可。

### 9.5 修复 404 页面 ###

如果访问不存在的页面，应该给出提示，这就是我们常说的 404 页面。在 404 页面中，还提供了 `Google Search` 的功能。但当我访问不存在的页面时，Google Search 却不生效。究其原因，原来是在绑定域名之前，我使用了 https 协议，对应的 Google Search JS URL 也应该是 https 形式的 URL。找到问题，解决之。

### 9.6 修复导航栏不能显示 ###

又一次对网站做了修改，但导航栏不再显示了。找了半天，找不到错误，而且也没有收到 Page Build Failure 错误。只得请教主题作者。原来是我在 Head 中添加的 JS 引用没有正确的闭合。

如果没有主题作者的帮助，很多问题只能依靠时间了。感谢 `Michael Rose`，每个问题都给我很好的回答。老外就是这样，办事效率高，一身 Geek 精神。

好了，问题就啰嗦到这里，如果有任何问题，欢迎评论或者发送邮件到 blockxyz@gmail.com。

## 十 后记 ##

这次建站经历于我而言是相当宝贵的，很多看似简单的问题，真正实施的时候未必如此。常言**知易行难**，这次感触颇深。把整个建站过程分享给大家，希望能给读者丁点启示，实乃欣慰。**更希望我在自己的小屋里好好写作，静心而为，大放异彩。**

Enjoy!

–EOF–

版权声明：自由转载-非商用-非衍生-保持署名<a href="http://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh" target="_blank">（创意共享4.0许可证）</a>
