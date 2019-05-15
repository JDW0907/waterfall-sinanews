##waterfall-sinanews
预览地址：
1.瀑布流新闻网：http://js.jirengu.com/jeduhizohi/1/
2.懒加载：http://js.jirengu.com/wapehohori/1/
3.瀑布流效果例子：http://js.jirengu.com/dulugazepa/1/
## 懒加载原理
-原理：先将img标签的src链接设为同一张图片（比如空白图片），然后给img标签设置自定义属性（比如 data-src）,然后将真正的图片地址存储在data-src中，当JS监听到该图片元素进入可视窗口时，将自定义属性中的地址存储到src属性中，从而达到懒加载的效果，这样能防止页面一次性向服务器发送大量请求，导致服务器响应慢，页面卡顿崩溃等。
## 瀑布流原理
-通过计算出一排能够容纳几列元素，然后寻找各列之中所有元素高度之和的最小者，并将新的元素添加到该列上，然后继续寻找所有列的各元素之和的最小者，继续添加至该列上，如此循环下去，直至所有元素均能够按要求排列为止。
##实现原理
###懒加载实现原理
1.获取窗口、窗口滚动和元素距离窗口顶部的偏移高度，计算元素是否出现在窗口可视范围内,元素显示的时候把之前的默认照片替换成data-src里的照片,或监听窗口滚动事件，检查元素是否在可视范围内，元素显示的时候把之前的默认照片替换成data-src里的照片。
2.判断浏览器滚动到最底部,当浏览器的高度 + 用户滚动的距离  = 页面的高度  就可以判断浏览器滚动到最低部了。
**代码示例**
**方法：**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="http://code.jquery.com/jquery-latest.js"></script>
</head>
<body>
    <div class="container">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="1" data-src="http://cdn.jirengu.com/book.jirengu.com/img/1.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="2" data-src="http://cdn.jirengu.com/book.jirengu.com/img/2.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="3" data-src="http://cdn.jirengu.com/book.jirengu.com/img/3.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="4" data-src="http://cdn.jirengu.com/book.jirengu.com/img/4.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="5" data-src="http://cdn.jirengu.com/book.jirengu.com/img/5.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="6" data-src="http://cdn.jirengu.com/book.jirengu.com/img/6.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="7" data-src="http://cdn.jirengu.com/book.jirengu.com/img/7.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="8" data-src="http://cdn.jirengu.com/book.jirengu.com/img/8.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="9" data-src="http://cdn.jirengu.com/book.jirengu.com/img/9.jpg">
        <h2>测试</h2>
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="10" data-src="http://cdn.jirengu.com/book.jirengu.com/img/10.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="11" data-src="http://cdn.jirengu.com/book.jirengu.com/img/11.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="12" data-src="http://cdn.jirengu.com/book.jirengu.com/img/12.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="13" data-src="http://cdn.jirengu.com/book.jirengu.com/img/13.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="14" data-src="http://cdn.jirengu.com/book.jirengu.com/img/14.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="15" data-src="http://cdn.jirengu.com/book.jirengu.com/img/15.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="16" data-src="http://cdn.jirengu.com/book.jirengu.com/img/16.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="17" data-src="http://cdn.jirengu.com/book.jirengu.com/img/17.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="18" data-src="http://cdn.jirengu.com/book.jirengu.com/img/18.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="19" data-src="http://cdn.jirengu.com/book.jirengu.com/img/19.jpg">
        <img src="http://smashinghub.com/wp-content/uploads/2014/08/cool-loading-animated-gif-3.gif" alt="20" data-src="http://cdn.jirengu.com/book.jirengu.com/img/20.jpg">        
    </div>
    <script>

    start()  //调用保证进入页面首页图片是可见的
    $(window).on('scroll',function() { 
       start() //页面滚动进行调用
    })// 页面滚动

    function start() {
        $('.container img').not('[data-isLoaded]').each(function() {//遍例img
                            //not 排除已经加载完成的图片
            var $node = $(this)
           if(isShow($node)) {
                setTimeout(function() {
                    loadImg($node)
                }, 500)
           }
       })
    }

    function isShow($node) {
        return $node.offset().top <= $(window).height() + $(window).scrollTop()
    }  //判断图片位置

    function loadImg($img) {
        $img.attr('src',$img.attr('data-src'))
        $img.attr('data-isLoaded',1) //对已经加载出来的图片添加属性
    }//进行图片加载
    </script>
</body>
</html>
```
###瀑布流实现原理

1.瀑布流图片/div容器的实现是通过对其进行绝对定位来实现的，假设X轴列有4张图片，宽度为100px; 那第一张left 值为0，第二张left值为100px，第三张为200px,第四张为300px;
2.图片的高度，我们需要通过对其图片的高度进行判断，让第二横对的图片首先放到 X 列高度最小的图片下面(如图所示，一横列为4张图片，第五张图片放在第二横列中，寻找到第二列的图片高度最低，就将图片当道第二列中。第6张图片寻找到第四列的高度低就将图片放到第四列中，下面每次也都是如此；
3.因为图片的高度很重要，我们需要保存并进行比较，所以我们要用一个数组来接受图片的高度。
**代码示例**
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="http://code.jquery.com/jquery-latest.js"></script>
</head>
  <style>
    .waterfall {
        max-width: 600px;
        margin: 0 auto;
        position: relative;
    }
    .waterfall img {
        width: 100px;
        margin: 10px;
        position: absolute;
        transition: all .4s;
    }

  </style>
<body>
<body>
    <div class="waterfall">
        <img src="http://via.placeholder.com/100x100" alt="300*40">
        <img src="http://via.placeholder.com/100x80" alt="300*100">
        <img src="http://via.placeholder.com/100x150" alt="300*100">
        <img src="http://via.placeholder.com/100x140" alt="300*100">
        <img src="http://via.placeholder.com/100x120" alt="300*100">
        <img src="http://via.placeholder.com/100x110" alt="300*100">
        <img src="http://via.placeholder.com/100x160" alt="300*100">
        <img src="http://via.placeholder.com/100x30" alt="300*100">
        <img src="http://via.placeholder.com/100x50" alt="300*100">
        <img src="http://via.placeholder.com/100x90" alt="300*100">
        <img src="http://via.placeholder.com/100x20" alt="300*100">
        <img src="http://via.placeholder.com/100x60" alt="300*100">
        <img src="http://via.placeholder.com/100x120" alt="300*100">
        <img src="http://via.placeholder.com/100x150" alt="300*100">
        <img src="http://via.placeholder.com/100x180" alt="300*100">
        <img src="http://via.placeholder.com/100x200" alt="300*100">
        <img src="http://via.placeholder.com/100x125" alt="300*100">
        <img src="http://via.placeholder.com/100x70" alt="300*100">
        <img src="http://via.placeholder.com/100x120" alt="300*100">
        <img src="http://via.placeholder.com/100x40" alt="300*100">
        <img src="http://via.placeholder.com/100x20" alt="300*100">
        <img src="http://via.placeholder.com/100x10" alt="300*100">
        <img src="http://via.placeholder.com/100x140" alt="300*100">

    </div>
    <script>

var colCount   // 列数
    var colHeightArray = []  //列高度的空数组
    var imgWidth = $('.waterfall img').outerWidth(true)
                                    //outerWidth(true) 表示元素所占用的全部的大小 左右边距等
    colCount = Math.floor($('.waterfall').width()/imgWidth)
    console.log(colCount)
    for(var i=0;i<colCount;i++) {
        colHeightArray[i] = 0
    } // 数组初始化为0 
    $('.waterfall img').on('load',function() {
            var minValue = colHeightArray[0]
            var minIndex = 0
            for(var i=0;i<colCount;i++) {
                if(colHeightArray[i]<minValue) {
                    minValue = colHeightArray[i]
                    minIndex = i
                }
            }
            $(this).css({
                left: minIndex * imgWidth,
                top: minValue
            })
        colHeightArray[minIndex]+=$(this).outerHeight(true)    
    })

    $(window).on('resize',function() {
        //jQuery 事件 - resize() 方法 
        //对浏览器窗口调整大小进行计数
        colHeightArray = []
        colCount = Math.floor($('.waterfall').width()/imgWidth)
        for(var i=0;i<colCount;i++) {
            colHeightArray[i] = 0
        } // 数组初始化为0 
        $('.waterfall img').each(function() {
            var minValue = colHeightArray[0]
            var minIndex = 0
            for(var i=0;i<colCount;i++) {
                if(colHeightArray[i]<minValue) {
                    minValue = colHeightArray[i]
                    minIndex = i
                }
            }
            $(this).css({
                left: minIndex * imgWidth,
                top: minValue
            })
            colHeightArray[minIndex]+=$(this).outerHeight(true) 
        })
    })
    </script>

</body>
</html>
```

