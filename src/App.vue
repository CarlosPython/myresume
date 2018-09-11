<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 源码地址 https://carlospython.github.io/myresume/
* 大家好，我是陈辉。
* 我来写一份简历！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(47,79,79);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始写简历 */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
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
  background: #ddd;
}
`, `/* 写个说明。
 * 感谢大家对我的关注。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #666666;
  color: #FFFFFF;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 25vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '>'; color: white;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, ">") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 25vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `Carlos
====

坐  标：杭州

93年跨境电商er，马拉松er一枚。

技能
----  

跨境电商
----
  - 独立运营Amazon
  - 团队搭建与管理
  - 独立创建跨境平台账户
  - 海外SNS全网营销与创建

外贸
----
  - 太阳能行业经验
  - 熟悉进出口流程
  - 客户开发与管理
 
PHOTOSHOP
----
  -  产品图片处理
  -  营销海报设计

其他
----
  - 英语  CET4  听说读写熟练
  - Sketchup 简单3D基础建模将想法可视化  
  - Python   在学，爬虫方向  为后续电商数据抓取提供技术基础便于进行数据化运营、新品开发分析
  - Power BI 数据可视化
  - 驾照 


工作经历
----

浙江雄泰光伏科技有限公司（1年2015）
----
  -  岗位： 技术员
  -  工作描述
  -  1.根据订单需求对太阳能组件完成CAD图纸设计BOM清单制作
  -  2.协助TUV认证和车间工艺技术支持
  -  3.参与实用新型专利设计项目

深圳英利新能源有限公司（3年 2015-2018）
----
  -  岗位： 外贸业务员 => 电商部主管 => 电商部经理
  -  工作描述
  -  1.负责Alibbaba平台管理及日常业务开发 （外贸业务员201510）
  -  2.负责Amazon/Lazada从0到1搭建与运营  (电商部主管201605）
  -  3.管理统筹公司电商/新媒体/营销板块   （电商部经理201704至201808）


教育经历
----
 - 南昌航空大学 [本科] 
 - 专业：光伏发电技术与应用


兴趣爱好
----
 - 马拉松
 - 书法
 - 看书听书
 - 乒乓球


我的博客
----

Minimalist  (用HEXO部署到Github的极简博客)  https://carlospython.github.io/

勾引方式
----

* 微信：chenhui153103

`, thanksMarkdown: `
自述
----


* 大学与太阳能专业结缘，后续从事了4年太阳能行业相关工作。从技术到业务到营销到管理一路走来成长了很多。权衡考虑，即将束近3年的深圳时光，前往杭州，因为爱情。
* 跨境电商工作其实是一个综合性很强的工作，营销、商业道德、会计、组织行为、数据分析等等都涵盖在内，个人目标是将自己锻炼成为一个MBA式思维方式的工作者。
* 未来，将仍然围绕电商进行更深度的尝试。16年因为公司发展需要与电商相识。
* 记得印象最深的一件事是，2017年在飓风玛丽亚9月袭击了波多黎各岛屿，当地电力基本都瘫痪了，由于没电当地非常非常的热。另外一方面发现有部分的美国亚马逊买家在购买太阳能风扇作为礼物送给自己在波多黎各的亲人，意识到了这个问题后，加大了FACEBOOK在这个地方营销投入和站内广告的投入，安排发邮件对已购买的客户表示关心与慰问，慢慢的波多当地人直接购买的人多了，而且复购率很高。很多人回邮件说简直要被热死了，这产品帮了他们很大的忙并表达了感谢。而店铺也完成了日销千刀的跨越。这件事后，让我觉得自己做的这件事变得有意义。所以后面，我想要用大数据算法分析根据地区舆论数据搜索热点，分析提高与产品开发的关联性，跨平台运营，将合适的产品交到需要的人手中，并让生活变得更美好。
* 我是乐观主义者，相信杭州将是一个新的起点和挑战。
* 最近在学习Python，前段时间偶然看到了Github南方大哥的项目，照着做了一个这样子IT风的简历，感觉很刺激。


  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>
