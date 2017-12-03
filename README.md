# 滚动到顶部固定
### 一、效果说明
单页的照片墙网页，风格如下：
- 整屏视频
- 瀑布流显示照片
- 视频滚动到顶部时固定，露出一部分做页眉

[点击查看模型](https://jiazhuamh.github.io/javascript/float.html)

[点击看效果](https://jiazhuamh.github.io/javascript/)

### 二、实现思路
#### 1. 使用bootstrap框架和JQuery
#### 2. 视频整屏设置
- 使用```container-fluid```去掉网页两边的白边
- 设置视频```border-bottom 20px```，和下面图片之间拉开一定距离
#### 3. 瀑布流照片墙
- 使用```col-md-4```设置三列
#### 4. 滚动悬停设置
```javascript

$(document).ready(function(){

    var dv = $('#fixbar');  // 滚动悬停的div 
    var st;   // 记录页面滚动了多少
    var width = dv.css('width');  // 记录原始的宽
    var height = dv.css('height') // 记录原始高
    var bottom = dv.outerHeight() - 60; // 留下视频底部60px的高度，悬停

    $(window).scroll(function() {
        st = Math.max(document.body.scrollTop || document.documentElement.scrollTop);
        if (st > bottom) {  // 如果滚动超过预设值
            dv.css({
                position: 'fixed',  // 位置设为固定
                top: -bottom, 
                width: width,
                height: height,
                zIndex: 999   // 覆盖下面照片

            });
            $('body').css({
                paddingTop: bottom + 60   // 因为div位置设成fixed，脱离文档流了，下面的内容会移上去，为了避免这样，设置body.padding-top填充上
            });
        } else if (dv.css('position') != 'static') {  // 如果又滚上去了
            dv.css({
                position: 'static',
            });
            $('body').css({
                paddingTop: 0
            });
        }
    });

});
```

