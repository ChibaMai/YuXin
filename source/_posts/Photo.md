---
title: 我的相册
id: 3
date: 2020-07-28 10:22:13
tags:
categories:
  - 语心
comments: false
peramlink: 3
---

我的相册，这里是我个人相册存储的地方

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>
<div class="photo">
  <div class="ui-timeLine">
    <div v-for="item in items" class="item">
      <div class="date" v-text="item.date"></div>
      <div class="line"></div>
      <div class="dot active"></div>
        <div class="box">
        <div class="cbox">
          <div class="title" v-text="item.title"></div>
          <div class="types">
            <a v-for="imgItem in item.type" :href="`/images${item.imgDate}${imgItem}.jpg`" target="_blank"><img :src="`/images${item.imgDate}${imgItem}.jpg`" alt data-action="zoom"></a>
          </div>
        </div>
      </div>
    </div>
    <div class="activeLine" style="height: 100%"></div>
  </div>
</div>

<script type="text/javascript">
(function($) {
  $.fn.uiTimeLine = function() {
    var $timeLine = $(".ui-timeLine");
    var $activeLine = $(".ui-timeLine .activeLine");
    var $dots = $(".ui-timeLine .dot");
    var $cboxs = $(".ui-timeLine .item .cbox");
    return this.each(function() {
      function setActiveLineHeight() {
        let height = $(document).scrollTop() + window.screen.height;
        let j = 0;
        for (let i = 0; i < $dots.length; i++) {
        if ($($dots[i]).offset().top < height) {
            $($($dots[i])).addClass("active");
            $($cboxs[i]).css({
              "left": 0
            });
            j = i;
          } else {
            $($($dots[i])).removeClass("active")
            $($cboxs[i]).css({
              "left": "100vw"
            });
          }
        }
        // $activeLine.css({
        //   "height": $($dots[j]).offset().top - $timeLine.offset().top + 10 + "px"
        // })
      }
      $(window).on('scroll', setActiveLineHeight);
      setActiveLineHeight();
    })
  };

})(jQuery);

</script>

<script>

setTimeout(function () {

  let mv = new Vue({
    el: ".ui-timeLine",
    data: {
      placeholder: "百度一下你就知道",
      items: [
        { 
          date: "2020 7/29", 
          title: "我的汉服照/嘿嘿女装照^_^", 
          imgDate: "/2020/7-29/",
          type: 6
        },
        { 
          date: "2020 6/2", 
          title: "南京风景图片", 
          imgDate: "/2020/6-2/",
          type: 15
        },
        { 
          date: "2020 5/28", 
          title: "开始留长发/我的游戏", 
          imgDate: "/2020/5-28/",
          type: 2
        },
         { 
          date: "2019 10/17", 
          title: "和小洋吃饭的照片", 
          imgDate: "/2019/10-17/",
          type: 1
        },
        { 
          date: "2019 10/16", 
          title: "北京市，东城区照片",
          imgDate: "/2019/10-16/",
          type: 8
        },

      ]
    },

    mounted() {
      $(".ui-timeLine").uiTimeLine();
    }
  });
}, 100)
</script>

<style>
.photo {

}

.ui-timeLine {
  padding: 50px 0;
  position: relative;
  overflow: hidden;
}

.ui-timeLine>.item {
  display: block;
  position: relative;
  text-align: justify;
  /* text-justify: newspaper; */
  word-break: break-all;
  padding-left: 70px;
  color: #555;
  padding-right: 10px;
}

.ui-timeLine>.item {
  padding-bottom: 20px
}

.ui-timeLine .active {
  border: 3px solid rgba(132, 43, 171, .8);
}

.ui-timeLine .line, .ui-timeLine>.activeLine {
  position: absolute;
  left: 54px;
  width: 4px;
  height: 100%;
  background-color: #eee;
}

.ui-timeLine .dot {
  z-index: 100;
  display: inline-block;
  position: absolute;
  left: 50px;
  top: 0;
  padding: 3px;
  /* border: 3px solid #eee; */
  border-radius: 20px;
  background-color: #fff;
  box-shadow: 3px 3px 8px #ccc;
  transition: .5s;
}

.ui-timeLine>.item>.box {
  padding: 5px 0;
}

.ui-timeLine>.item::after {
  content: "";
  display: block;
  clear: both;
}

.ui-timeLine>.item .cbox {
  position: relative;
  left: 100vw;
  transition: left 1s;
  padding: 10px;
  border-radius: 10px;
  /* background-image: linear-gradient(45deg, rgba(0, 200, 255, 0.4) 0%, rgba(132, 43, 171, 0.4) 100%); */
  box-shadow: 3px 3px 8px #ccc;
}

.ui-timeLine .date {
  width: 40px;
  font-size: 14px;
  position: absolute;
  left: 10px;
  top: -7px;
}

.ui-timeLine .title {
  font-size: 16px;
  font-weight: 900;
  line-height: 30px;
  padding: 5px 0 10px 0; 
}

.ui-timeLine .types>span {
  font-size: 10px;
  border-radius: 5px;
  padding: 2px 10px;
  margin-right: 10px;
  border: 1px solid #fff;
}

.ui-timeLine>.activeLine {
  background-color: rgba(0, 200, 255, .8);
  z-index: 50;
  top: 50px;
  height: 0;
  max-height: calc(100% - 80px);
  transition: height 1s;
  box-shadow: 3px 3px 2px #eee;
}

.types{
  display: flex;
  flex-wrap: wrap;
}

.types a {
  width: 140px;
}

img {
  width: 100%;
  /* height: 100% */
} 
</style>
