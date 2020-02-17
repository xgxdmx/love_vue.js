<template>
    <div id="app">
        <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
        <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
</template>
<script>
import StyleEditor from './components/StyleEditor'
import ResumeEditor from './components/ResumeEditor'
import './assets/reset.css'
let isPc = (function() {
    var userAgentInfo = navigator.userAgent;
    var overrideBrowserslist = ["Android", "iPhone",
        "SymbianOS", "Windows Phone",
        "iPad", "iPod"
    ];
    var flag = true;
    for (var v = 0; v < overrideBrowserslist.length; v++) {
        if (userAgentInfo.indexOf(overrideBrowserslist[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}());
let getDateDiff = function(startDate, endDate) {
    var startTime = new Date(Date.parse(startDate.replace(/-/g, "/"))).getTime();
    var endTime = new Date(Date.parse(endDate.replace(/-/g, "/"))).getTime();
    var dates = Math.abs((startTime - endTime)) / (1000 * 60 * 60 * 24);
    return dates;
}
document.title += getDateDiff((new Date()).getFullYear() + '-' + ((new Date()).getMonth() + 1) + '-' + (new Date()).getDate(), '2017-12-30') + 1 + '天';
export default {
    name: 'app',
    components: {
        StyleEditor,
        ResumeEditor
    },
    data() {
        return {
            interval: 27,
            currentStyle: '',
            enableHtml: false,
            fullStyle: [
                `/*
* 馨颖，好久不见了！
* 说真的，不知道最近是因为荷尔蒙的暴增还是什么其他原因，
* 感觉没有你在的日子真的是度日度年
* 但，最近这情况，即使这样我也不能因为我的私心，对吧！
* 你的健康真的比什么都重要！
* 虽说不能出来了，但该过的节日咱还是要过的。
* 毕竟生活还是应该要有一些仪式感！
* 所以，唉，也想不出什么新鲜玩意儿。
* 最近在家都待傻了。
* 所以，请允许我用比较直男，比较硬核，比较程序员的方式表白（づ￣3￣）づ╭❤～
* 不过首先，说起来手机和电脑还得区分一下。
* 你现在用的是。。。${isPc ? '不大可能打开的笔记本' : '宅家三件套之一的手机'}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了。来点背景 */
html {
  color: rgb(222,222,222);
  background: rgb(255,182,193);
}
/* 文字太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  font-size: 14px;
  line-height:1.5;
}
/* 这些代码颜色都一样。加点儿高亮区别来 */
.token.selector{ color: rgb(133,153,0) }
.token.property{ color: rgb(187,137,0) }
.token.punctuation{ color: yellow }
.token.function{ color: rgb(42,161,152) }
.token.comment{ color: rgb(177,177,177) }
/* 加个 3D 效果 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; 
  ${ isPc ? 'left: 0;' : 'left:0;right:0;margin:auto;'}
  top: 0; 
  -webkit-transition: none; 
  transition: none;   
  ${ isPc ? '-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;' }
  ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed; 
  ${ isPc ? 'right: 0;' : 'left:0;right:0;margin:auto;'}
  ${ isPc ? 'top: 0;' : 'bottom:2%;'}
  padding: .5em;  
  ${ isPc ? 'margin: .5em;' : ''}
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 14px;
  line-height:1.5;
  ${ isPc ? '-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;' }
    ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
  }
/* 我开始写了 */


`,
                `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 */
`,
                `
/* 再加点样式 */
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;            
  content: counters(section, ".") " ";  
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: rgba(221,221,221,.5);
}

/* OK。完成！ */

`
            ],
            currentMarkdown: '',
            fullMarkdown: `石运 × 谈馨颖
----

2016年。初次见面，请多关照。
2017年12月30日。我们终于官宣啦，终于可以撒狗粮啦！
已有 \`${getDateDiff((new Date()).getFullYear()+'-'+((new Date()).getMonth()+1)+'-'+(new Date()).getDate(),'2017-12-30') + 1}\` 天

在这\`${getDateDiff((new Date()).getFullYear()+'-'+((new Date()).getMonth()+1)+'-'+(new Date()).getDate(),'2017-12-30') + 1}\` 天里，我们经历了许多

我们一起看了一些电影
----

* 烟花
* 哆啦A梦
* 千与千寻
* 天气之子
* 紫罗兰永恒花园外传：永远与自动手记人偶
我们一起去了一些餐厅吃饭
----

* 大悦城
* 宜家
* 韩盛古法烤肉
* 遇约烤鸭
* ......

我们一起玩一些游戏，虽然我菜的一批
----

* 和平精英
* 穿越火线
* 王者荣耀
* ......

你还送给我很多礼物
----
1. 阿狸抱枕
2. 阿狸手捂
3. 阿狸毛毯
4. 零食大礼包
5. 你的名字小说
6. 你的名字拼图
7. 韩国折扇
8. 回车键
9. 化妆品
10. 靠垫
11. 一个小石头
......

#### 但其实，最好的礼物就是我这辈子遇见了你，你是我的女朋友。
#### 我其实，还一直在由于一件事，就是那封信。但当我看完我的电子稿后，我便发现一件比较可笑的事情。
#### 我在最终落笔的时候，又有了一些改动，所以那份我亲笔信件，是这个世界上唯一一份。连身为作者的我都无法复制。
#### 我真的不是很善于言表，写的东西也都是开水白菜，没滋没味。这一直以来是我的缺点之一。我也在努力改进。
#### 所以，最后在2020年里，即使开场就是全人类的不幸，但没有办法，时间不给你退货。我依然是你的zzbb。

> 我想做的，不仅仅是作为你的男朋友，我更想改变你的人生。幸福是每个人都应该享有的东西。
> 所以，我向你发誓，我会给予你一个幸福的生活，一个温暖的港湾（家）！爱你（づ￣3￣）づ╭❤～

`
        }
    },
    created() {
        this.makeResume()
    },

    methods: {
        makeResume: async function() {
            await this.progressivelyShowStyle(0)
            await this.progressivelyShowResume()
            await this.progressivelyShowStyle(1)
            await this.showHtml()
            await this.progressivelyShowStyle(2)
        },
        showHtml: function() {
            return new Promise((resolve, reject) => {
                this.enableHtml = true
                resolve()
            })
        },
        progressivelyShowStyle(n) {
            return new Promise((resolve, reject) => {
                let interval = this.interval
                let showStyle = (async function() {
                    let style = this.fullStyle[n]
                    if (!style) {
                        return
                    }
                    // 计算前 n 个 style 的字符总数
                    let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
                    let prefixLength = length - style.length
                    if (this.currentStyle.length < length) {
                        let l = this.currentStyle.length - prefixLength
                        let char = style.substring(l, l + 1) || ' '
                        this.currentStyle += char
                        if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                            this.$nextTick(() => {
                                this.$refs.styleEditor.goBottom()
                            })
                        }
                        setTimeout(showStyle, interval)
                    } else {
                        resolve()
                    }
                }).bind(this)
                showStyle()
            })
        },
        progressivelyShowResume() {
            return new Promise((resolve, reject) => {
                let length = this.fullMarkdown.length
                let interval = this.interval
                let showResume = () => {
                    if (this.currentMarkdown.length < length) {
                        this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
                        let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
                        let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
                        if (prevChar === '\n' && this.$refs.resumeEditor) {
                            this.$nextTick(() => this.$refs.resumeEditor.goBottom())
                        }
                        setTimeout(showResume, interval)
                    } else {
                        resolve()
                    }
                }
                showResume()
            })
        }
    }
}
</script>
<style scoped>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

html {
    min-height: 100%;
}
.styleEditor {
    -webkit-backface-visibility: hidden;
}
</style>
