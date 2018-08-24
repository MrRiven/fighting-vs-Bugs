# 看完你就变菜了v1.0

1. ios 端滑动不顺滑的问题解决

   `-webkit-overflow-scrolling` 属性控制元素在移动设备上是否使用滚动回弹效果. 

    `auto`: 使用普通滚动, 当手指从触摸屏上移开，滚动会立即停止。

    `touch`: 使用具有回弹效果的滚动, 当手指从触摸屏上移开，内容会继续保持一段时间的滚动效果。继续滚动的速度和持续的时间和滚动手势的强烈程度成正比。同时也会创建一个新的堆栈上下文。

   

2. 移动端隐藏滚动条

   **::-webkit-scrollbar {display: none;}**  其他属性的使用自行百度, 定制 scrollbar

   

3. 移动端 window.onscroll 无法触发问题  ||  页面scroll 无法触发

   ```js
    window.onscroll = scroll
       function scroll() {
         let top = document.documentElement.scrollTop || document.body.scrollTop
         if (top > 88) alert('我触发了')
       }
   
   在移动端,要操作页面的滚动的话,只有 document.body.scrollTop 能触发, 在 pc 则不行;
   在 pc 端, 只有 document.documentElement.scrollTop 能触发
   ```

   

4. css 去除input  textarea 的阴影

   ```css
   input,textarea{-webkit-appearance: none;appearance: none;}
   ```

   

5. 1px 的解决方案

   我在微信端 和  混合 app 中都遇到过这个问题,常规解决方案用小数,但是还是有问题;

   在混合 app中, 0.5px 的 border 在 ios 端无法显示, 在 Android端正常显示,

   在微信端 , 会被放大.

   解决方案:  css 解决 

   ```css
   /* 圆角(伪类和本体类都需要加border-radius) */
   /* 盒子边框 */
   .borderRadius-1px {
       border: none;
       position: relative;
   }
   
   .borderRadius-1px:after {
       content: "";
       position: absolute;
       top: 0;
       left: 0;
       border: 1px solid #e8e8e8;
       -webkit-box-sizing: border-box;
       box-sizing: border-box;
       width: 200%;
       height: 200%;
       -webkit-transform: scale(0.5);
       transform: scale(0.5);
       -webkit-transform-origin: left top;
       transform-origin: left top;
       border-radius: 0.16rem;
       -webkit-border-radius: 0.16rem;
       -moz-border-radius: 0.16rem;
       -ms-border-radius: 0.16rem;
       -o-border-radius: 0.16rem;
   }
   
   /* 上边框, 同理可得下 左  右*/
   .scale-1px-top {
       border: none;
       position: relative;
   }
   
   .scale-1px-top:after {
       content: "";
       position: absolute;
       display: block;
       top: -1px;
       left: 0;
       width: 200%;
       height: 1px;
       border-bottom: 1px solid #e8e8e8;
       -webkit-transform: scale(0.5, 0.5);
       transform: scale(0.5, 0.5);
       -webkit-transform-origin: 0 0;
       transform-origin: 0 0;
       z-index: 2;
       -moz-transform: scale(0.5, 0.5);
       -ms-transform: scale(0.5, 0.5);
       -o-transform: scale(0.5, 0.5);
   }
   
   
   ```

   **这个 css 解决方案有个弊病, 它是用伪元素来做的, 所以在项目之初, 你就需要知道该1px 的解决方案使用的伪元素是哪个, 避免在页面编写中发生冲突.  并且, 清除浮动会将其清除, 你懂得. **

6. 