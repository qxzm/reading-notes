## SMACSS



#### SMACSS简介

> Scalable and Modular Architecture for CSS
>
> 可扩展的，模块化的CSS架构。是一个指南，一个CSS设计的最佳实践

参考 [Scalable and Modular Architecture for CSS](http://smacss.com/)



#### SMACSS最佳实践

1. ##### 分类CSS规则

   * **Base**		默认的css规则，Normalize或者Reset之类

     ```css
     1 html, body, form { margin: 0; padding: 0; }
     2 input[type=text] { border: 1px solid #999; }
     3 a { color: #039; }
     4 a:hover { color: #03C; }
     ```

   * **Layout**     负责页面的布局，可包含多个Module

   * **Module**    模块化的，可重用的css规则，菜单，列表，组件等

   * **State**         描述的是Layout或者Module的特殊状态，active，hidden等

   * **Theme**      指的是所有Layout或者Module的主题

2. ##### 规范命名规则

   * 对于**layout**规则，一般使用 l- 或 layout- 作为前缀。
   * 对于**state**规则，一般使用 is- 作为前缀，比如 .is-hidden 或 .is-collapsed 。
   * 对于**modules**规则，作为最主要的一类css规则，SMACSS建议直接使用module名称，不需要任何前缀

3. ##### 选择符书写建议

   * CSS选择符是从右向左匹配的，四个主要的效率低下规则为
     * 带有后代选择器的规则。例如`#content h3`
     * 带子或相邻选择器的规则。例如`#content > h3`
     * 具有过度合格选择器的规则。例如`div#content > h3`
     * 适用`:hover`于非链接元素的规则。例如`div#content:hover`
   * 建议
     * 使用子选择器
     * 避免使用常用元素的标签选择器
     * 使用类名作为最右侧的选择器



#### CSS Rule Categories 详解

1. ##### Base

   > 所有元素的默认styles，可以理解为为了屏蔽浏览器的差异，对所有元素重新定义的一类CSS

   1.1 **代码展示**

   ```css
   body, form {
   	margin: 0;
   	padding: 0;
   }
   a {
   	color: #039;
   }
   a:hover {
   	color: #03F;
   }
   ```

   1.2 **最佳实践**

   * Base Rules 可以出现
     * element selector		元素选择器
     * descendant selector  后代选择器
     * child selector               子选择器
     * pseudo selector          伪类选择器
     * attribute selector        属性选择器
   * 不应该出现
     * class selector				类选择器
     * ID selector                     ID选择器
     * !important

2. ##### Layout

   > 指用于布局的CSS。应该区分布局和内容，并且将内容抽象为Module，Module只关心自己的形状，至于放在哪里是它的容器Layout应该做的事

   2.1 **代码展示**

   ```css
   .l-grid {
       margin: 0;
       padding: 0;
       list-style-type: none;
   }
   .l-grid > li {
       display: inline-block;
       margin: 0 0 10px 10px;
   }
   ```

   2.2 **最佳实践**

   * 避免ID选择符
   * 对Module只指定布局信息，不对Module的内容信息做处理

3. ##### Module

   > 重复使用的元件模组，可以认为是component

   3.1 **代码展示**

   ```css
   .module > h2 {
       padding: 5px;
   }
   
   .module span {
       padding: 5px;
   }
   ```

   3.2 **最佳实践**

   * 避免ID选择器
   * 避免元素选择器，如果元素选择器是可预测的，使用具有元素选择器的子选择器或者后代选择器

4. ##### State

   > 状态是增强和覆盖所有其他样式的东西，通常应用于布局规则相同的元素，或应用于Base相同的元素

   4.1 **代码展示**

   ```css
   .tab {
       background-color: purple;
       color: white;
   }
   
   .is-tab-active {
       background-color: white;
       color: black;
   }
   ```

   4.2 **最佳实践**

   * State应该独立，通常由单一类选择器构成
   * 允许或者说推荐使用**!important**
   * 在为特定Module制定State规则时，State名称应包括其中的Module名称，规则也应包含

5. ##### Theme

   > 主题，应可以影响任何其他类型的CSS Rule

   5.1 **代码展示**

   ```css
   /*in module-name.css*/
   .mod {
       border: 1px solid;
   }
   
   /*in theme.css*/
   .mod {
       border-color: blue;
   }
   ```

   5.2 **最佳实践**

   



