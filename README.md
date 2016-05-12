# All about left-pad

如何看待 left-pad 事件？

先介绍一下我所在的公司。百姓网，做分类信息的，58赶集合并后自动排名上升一位，今年刚刚在新三板上市。如有兴趣，可投简历给我：heshijun@baixing.com（硬广告完毕。）

然后介绍一下我自己：
github: @hax
weibo: @johnhax
zhihu: 贺师俊
（特别的，我刚刚在知乎上有个回答过6000赞，欢迎大家继续点赞，哈哈。）

大家熟悉我的知道，我经常讲一些有“争议性”的话题，比如：
去年讲的 JavaScript: The World's Best Programming Language
http://johnhax.net/2015/js-the-best/
今年也讲过 程序员的圣战之 TAB vs SPACE
http://johnhax.net/2016/tab-vs-space/

通常对于有争议的话题，有两种典型态度：
回避
嘲笑

left-pad 事件也是如此。

先简单回顾一下 left-pad 事件。

简单说，就是一个叫 Azer 的开发者因为 npm 公司把本来他持有的 kik 包名字转移给了 kik 公司，一怒之下 unpublish 了他的所有包。其中一个叫 left-pad 的包，被 babel、react native 等依赖，于是它们就安装失败了，进而所有依赖它们的应用也都会安装和构建失败。

注：Kik 是一个类似微信的 App，据说微信当初也参考了它，且腾讯去年投资了该公司 5000万美元。

详细一点的，这里有两个链接大家可以看看，一个是英文的，一个是中文的：
- [How one developer just broke thousands of projects](http://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/)
- [开发者对 npm 公司不满，unpublish 了自己的所有模块](http://zhuanlan.zhihu.com/p/20669077)

大家可以看到英文文章的标题是 How one developer just broke thousands of projects。实际上因为 left-pad 这个包的真正执行代码其实只有 11 行（排除了空行），所以甚至有 11 lines code break the Internet 这样耸人听闻的说法。

当然这是标题党了。比如，广大中国开发者其实压根没有受到影响。因为这个事件发生在北京时间早上 5:30，到 8 点之前 npm 官方就解决了。

即使受到影响的人，也只是安装包和构建失败，并不会产生任何线上事故。

不过这个事件还是引发了大量的讨论。最著名的一篇技术评论文章是：
Have We Forgotten How To Program? http://www.haneycodes.net/npm-left-pad-have-we-forgotten-how-to-program/
中译：我们是不是早已忘记该如何好好地编程？ http://zhuanlan.zhihu.com/p/20707235

这文章再一次提出了对 node.js/npm 社区的小模块文化的批评，除了 left-pad 之外，还举了只有一行代码的 isArray ，和只有 4 行代码却有 3 个依赖的 is-positive-integer 作为反面典型。

文章的小标题也代表了他的观点：一个函数并不能被称为模块、第三方依赖带来的问题、我们应该尽可能减少依赖的模块。

类似论点的文章国内外都有许多，这里不一一列举，仅列一下知乎上相关的问题：
- [如何看待 Azer Koçulu 删除了自己的所有 npm 库？](https://www.zhihu.com/question/41694868)
- [NPM中将函数当作一个包发布的方式是否合理？](https://www.zhihu.com/question/41750206)
- [如何评价《The current state of JS programming》？](https://www.zhihu.com/question/42906029)

其中《The current state of JS programming》比较有趣，属于高端黑。

不过我想先提一个小问题。如果说“一个函数并不能被称为模块”，那到底几个函数可以成为一个模块呢？三个可不可以？两个可不可以？边界在哪里？



在技术讨论以外，也出现了行为艺术。比如
- [left-pad as Service](http://left-pad.io/)
- [Gives you five](http://fivejs.lol/)
- [is 13?](https://github.com/jezen/is-thirteen)

甚至其他语言平台的程序员也加入了狂欢，争相移植 left-pad：
- [Ruby](https://github.com/Somsubhra/left-pad)
- [C#](https://github.com/EgorBo/left-pad-net)
- [Rust](https://github.com/futile/leftpad-rs)
- [Haskell](https://hackage.haskell.org/package/acme-left-pad

不过我要说，有些移植实在是太偷懒了，比如 Ruby 移植，直接调用了 Ruby 内建的 rjust 方法。对此，我觉得讽刺也应该认真一点，否则只会显得比你要讽刺的对象更 low。

回到我一开始讲的，对于有争议的话题，很容易滑向“回避”和“嘲笑”。因为这是最省力的方法。就这一点来说，我的态度是：

我就是认真。

因此就有了我这个话题分享。


以下是我根据所看到的各方讨论所总结的一些话题。

## 如何看待 left-pad 事件？

- 谁是这次事件的罪魁祸首？azer？kik 公司？npm 公司？
- azer 是英雄还是熊孩子？
- npm 公司是不是邪恶的公司？
- 开源是不是注定不靠谱？
- 包是不是应该有命名空间？
- 我们都忘记怎么编程了吗？
- 小模块是好是坏？
- leftpad 本身应该怎么实现？
- 第三方依赖是好是坏？
- 是不是应该使用 shrinkwrap/lock（锁定依赖）？
- 是不是应该使用 bundle/pack（打包依赖）?
- 是不是应该自建仓库？
- js/nodejs/npm/前端…… 生态是不是有问题？


因为分享时间有限，不能全部讨论，我尽量能讲多少讲多少吧。未尽之处，我们可以以后再找时间讨论。

先说这几个相关的问题：

- 谁是这次事件的罪魁祸首？azer？kik 公司？npm 公司？
- azer 是英雄还是熊孩子？
- npm 公司是不是邪恶的公司？

我本来以为大多数人会认为 Kik 公司欺压开源作者，所以会归罪于 Kik。但实际调查下来，大多数人觉得这个锅应该是 npm 公司背。既然觉得 npm 公司是罪魁祸首，那么按逻辑说，应该认为 Azer 是反抗暴政的英雄才对。不过实际调查结果并不是这样。这样一种矛盾的调查结果，也许反应了大家在对待这个事情的时候更多是诉诸于感情从而产生了矛盾的情形。

我们优秀的工程师之所以优秀，是因为他们擅长做事实判断，比如代码写得是不是正确，性能好不好，口说无凭，得写测试。feature有用还是没用，数据说话。不过要价值判断的时候，就往往有点问题了。

比如……

百度的例子。

这个价值观的问题……

言归正传，要进行价值判断很困难，但是至少我们先搞清楚事实。

这里有个：Azer NPM 撤包事件全信件 http://zhuanlan.zhihu.com/p/20671763

这里翻译了 Azer/Kik/NPM 的来往邮件。大家可以看看。

看了之后，是不是觉得 Kik 很可恶呢？

不过在此之前，我们最好看下评论。比如第五页上尤雨溪的评论。

尤雨溪是 Vue.js 的作者，目前在美国 Meteor 公司供职，在美国生活了 10 年。他对英语原文的理解应该是比较准确的，不过译者孙志贵也在加拿大生活过 4 年，所以作为英语渣渣的我其实很难直接判断到底谁说的对。然而，孙志贵自己表示了他的立场，基本上就是认为 Azer 是英雄，Kik 是流氓，NPM 是是是非不分助纣为虐的邪恶公司。所以我倾向于认为这是一个立场先行的翻译。

另外，尤雨溪也提出，这里缺少了 NPM 官方回应（blog）的翻译。当然，孙志贵这个特辑本来也就是“全信件”，不翻译 npm 的 blog，也不好责难他。但是如果你要完整的了解事情，不看 npm 官方的表述，恐怕也很难全面的认识。

下面是一些第一手的资料链接：

- [A discussion about the breaking of the Internet](https://medium.com/@mproberts/a-discussion-about-the-breaking-of-the-internet-3d4d2a83aa4d#.mbd6n33vb)
- [I’ve Just Liberated My Modules](https://medium.com/@azerbike/i-ve-just-liberated-my-modules-9045c06be67c#.82gz6vy03)
- [kik, left-pad, and npm](http://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm)

第一个链接是 Kik 公司的 CEO 写的。
