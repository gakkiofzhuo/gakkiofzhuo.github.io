---
title: about
date: 2018-12-12 22:14:36
keywords: 关于
description: 
comments: false
photos: https://cdn.jsdelivr.net/gh/honjun/cdn@1.4/img/banner/about.jpg
---
{% raw %}
<div class="moe-mashiro" style="text-align:center; font-size: 50px; margin-bottom: 20px;">[桜の季節:刘小宅]</div>
<div id="hello-mashiro" class="popcontainer" style="min-height: 300px; padding: 2px 6px 4px; background-color: rgba(242, 242, 242, 0.5); border-radius: 10px;">
  <center>
  <p>
  </p>
  <h4>
  与&nbsp;<ruby>
  刘小宅&nbsp;<rp>
  （</rp>
  <rt>
  真（ま）白（しろ）</rt>
  <rp>
  ）</rp>
  </ruby>
  对话中...</h4>
  <p>
  </p>
  </center>
  <bot-ui></botui>
</div>
<script src="https://cdn.jsdelivr.net/vue/latest/vue.min.js"></script>
<script src="https://unpkg.com/botui/build/botui.min.js"></script>
<script>
function bot_ui_ini() {
    var botui = new BotUI("hello-mashiro");
    botui.message.add({
        delay: 800,
        content: "Hi, little lovers ~~~👋"
    }).then(function () {
        botui.message.add({
            delay: 1100,
            content: "这里是 刘小宅"
        }).then(function () {
            botui.message.add({
                delay: 1100,
                content: "一个可爱的蓝孩子~"
            }).then(function () {
                botui.action.button({
                    delay: 1600,
                    action: [{
                        text: "然后呢？ 😃",
                        value: "sure"
                    }, {
                        text: "少废话！ 🙄",
                        value: "skip"
                    }]
                }).then(function (a) {
                    "sure" == a.value && sure();
                    "skip" == a.value && end()
                })
            })
        })
    });
    var sure = function () {
            botui.message.add({
                delay: 600,
                content: "😘"
            }).then(function () {
                secondpart()
            })
        },
        end = function () {
            botui.message.add({
                delay: 600,
                content: "![...](https://view.moezx.cc/images/2018/05/06/a1c4cd0452528b572af37952489372b6.md.jpg)"
            })
        },
        secondpart = function () {
            botui.message.add({
                delay: 1500,
                content: "目前快要毕业于东南大学"
            }).then(function () {
                botui.message.add({
                    delay: 1500,
                    content: "向往技术却误入二次元，但后来喜欢上了日本的生活…"
                }).then(function () {
                    botui.message.add({
                        delay: 1200,
                        content: "因为要实现梦想还是需要Coding"
                    }).then(function () {
                        botui.message.add({
                            delay: 1500,
                            content: "主攻 Java语言 和 Python，略懂 Linux，偶尔也折腾 HTML/CSS/JavaScript/PHP"
                        }).then(function () {
                            botui.message.add({
                                delay: 1500,
                                content: "研究的方向，是成为一名全栈工程师（Full Stack Developer）以及机器学习（machine learning）"
                            }).then(function () {
                                botui.message.add({
                                    delay: 1800,
                                    content: "喜欢画画，希望有一天能够画出满意的新垣结衣的肖像"
                                }).then(function () {
                                    botui.action.button({
                                        delay: 1100,
                                        action: [{
                                            text: "为什么叫刘小宅呢？ 🤔",
                                            value: "why-mashiro"
                                        }]
                                    }).then(function (a) {
                                        thirdpart()
                                    })
                                })
                            })
                        })
                    })
                })
            })
        },
        thirdpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "因为本人比较宅，喜欢逛B站，喜欢的番剧有：玉子爱情故事、四月是你的谎言、千反田等~"
            }).then(function () {
                botui.action.button({
                    delay: 1500,
                    action: [{
                        text: "博客是喜欢纸片人呢？还是三次元呢？ 🤔",
                        value: "why-like"
                    }]
                }).then(function (a) {
                    fourthpart()
                })
            })
        },
        fourthpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "额，这个问题不好回答，纸片人和三次元还是不同的，不过小宅朋友不多，但是喜欢交朋友"
            }).then(function () {
                botui.message.add({
                    delay: 1100,
                    content: "而且我真的很友好，虽然话不多，性格比较腼腆~~"
                }).then(function () {
                    botui.action.button({
                        delay: 1500,
                        action: [{
                            text: "域名有什么含意吗？(ง •_•)ง",
                            value: "why-domain"
                        }]
                    }).then(function (a) {
                        fifthpart()
                    })
                })
            })
        },
        fifthpart = function () {
            botui.message.add({
                delay: 1E3,
                content: "emmmm，因为喜欢gakki，我另外的技术博客中有一个gakki的视频，可以去瞅瞅~~"
            }).then(function () {
                botui.message.add({
                    delay: 1500,
                    content: "还有什么想问的，可以留言噢，欢迎大家常来~~"
                }).then(function () {
                    botui.message.add({
                        delay: 1600,
                        content: "那么，仔细看看我的博客吧？ ^_^"
                    	})
                	})
                })
        } 
}
bot_ui_ini()
</script>

{% endraw %}