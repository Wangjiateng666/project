# CSS要点

## 盒子模型

* 行内元素的margin是相加的
* 块级元素 当两个块级元素的作用域在同一个地方,取最大值
* 兼容性问题:
  * W3C标准盒子模型的大小是往外扩
  * IE浏览器的盒子模型的大小是往里缩

## 字体

* em和百分比的区别
  * 百分比仅限于字体大小,不能跨属性
  * em是根据父元素的字体大小来设置的
  * font-style:italic 字体倾斜
  * vertical-align:top|middle|bottom 垂直对齐方式
  * letter-spacing 设置字与字之间的间距
  * text-decoration 字体下划线
    * underline 字体下划线
    * line-through 字体删除线

## 浮动

* 让当前的元素脱离文档流,同时会影响后面元素的显示方式,并且后面元素在显示的时候会把当前元素的位置空出来
* 空出来的只有内容,北京不会被空出来

## 背景图片

* background-attachment:fixed 固定背景图片
* background-position:
  * 设置单词->上下,左右
  * 设置百分比->水平,垂直
  * 设置像素->右下角是两个负数
* writing-mode:tb-rl 竖向文字

## 表单

* border-collapse:collapse 属性设置表单的边框是否被合并为一个单一的边框
* :hover 一般会在超链接上面使用,在其他元素上面会出现兼容性问题

## CSS形容超链接

* 注意书写顺序,:link>:visited>:hover>:active

## 隐藏内容

* visibility:hidden|visible

## 定位

* 绝对定位的元素可以叠加,相对定位的元素不可以重叠

## 清除浮动

* clear:both
* 给父元素添加高度
* overflow:hidden
  * 给父元素添加这个属性
  * hidden scroll auto这三个属性都可以
* BFC(块级元素上下文) 父元素在计算高度的时候,会把浮动的子元素的高度计算进去

## 布局方式

## PC

* 固定浮动布局
  * 不随窗口变化而变化
  * 主要使用float进行布局
  * 缩放窗口不会影响网页布局
  * 采用margin:0 auto方式进行居中
* 固定定位布局
  * 不随窗口变化而变化
  * 主要使用position:absolute进行定位
  * 缩放窗口不会影响网页布局
  * 采用position:absolute拉回方法进行居中

## 打开无线热点

* 设置 `netsh wlan set hostednetwork mode=allow`

  ` ssid=yfzxm key=1111112222`

* 打开 `netsh wlan strat hostednetwork`

* 关闭 `netsh wlan stop hostednetwork`

* 禁止 `netsh wlan set hostednetwork mode=disallow`

## CSS兼容性
* webkit Chrome safari
* presto Opera
* Trident IE
* gecko firefox

## CSS Hack
* `CSS Hack`我们为了页面的统一效果,就需要针对不同的浏览器或不同的版本写特定的CSS样式,我们把这个针对不同浏览器/不同版本写相应的`CSS CODE`的过程叫做`CSS Hack`
* CSS属性前缀法
* 选择器前缀法
* IE条件注释法

## IE条件注释法

* 只在IE下生效
* `<!--[if IE]>这段文字只能在IE浏览器显示<![endif]-->`
* 只在`IE6`下生效
* `<!--[if IE 6]><![endif]-->`
* 在`IE6`以上版本生效
* `<!--[if gte IE 6]><![endif]-->`
* 在`IE8`版本不生效
* `<!--[if ! IE 8]><![endif]-->`

## CSS属性前缀法

* `*`  `IE6,7`
* `_`  `IE5,6`
* 上面写的是写在`CSS`属性上面`_color:red`,下面是写在CSS属性值后面`height:120px\9`
* \9 6-11
* \0 5-11
* \9\0 8-10

## 选择器属性前缀

* `-ms` IE内核
* `-moz` 火狐
* `-o` Opera
* `-webkit` 谷歌

## `IE6` IE常见BUG

1. 双边距问题
   * 给父元素设置浮动,子元素也设置浮动,就会出现双倍的情况
   * 解决:给父元素设置`display:inline;`
   
2. 3像素BUG
   
   * 第一个元素左浮动,第二个不设置会造成3px
   * 解决:第二个元素浮动
   
3. 图片下面有空隙

   * 上面设置一个图片,下面是一个块状元素,会造成3px
   * 解决:给图片添加`display:block`

4. 空元素的高度问题1

   * 如果一个元素没有任何内容,高度在0-19px之内
   * 解决:`font-size:0px;`  或者 `overflow:hidden`

5. 超链接文本动态效果展示

   * 解决:`a:link a:visited a:hover a:active`

6. li外边距问题

   * 当li标记最后一个子元素设置浮动每个li之间会产生`3px`间距
   * 解决:vertical-align:top;

7. png图片背景透明问题

   ```css
   <!--[if IE 6.0]>
   	<script type="text/javascript" src="DD_belatedPNG.js"></script>
   	<script type="text/javascript">
   		DD_belatedPNG.fix('img');
   	</scirpt>
   <![endif]--!>
   ```

## CSS3

## 媒介查询

```css
@media screen and (min-width:480px){}
<link xxxx media="only screen and (max-width:xxxpx)">
```

## css的裁剪clip

1. 首先你要注意：**clip属性只能在元素设置了"position:absolute"或者"position:fixed"属性起作用。**
2. 使用：clip:rect(`<top>,<right>,<bottom>,<left>`)
3. 超出部分不显示内容
4. 当top和left取值为auto的时候，相当于0
5. 当bottom和right取值为auto的时候，相当于100%


















































