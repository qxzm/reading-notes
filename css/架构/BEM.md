## BEM

> **BEM**的意思就是块（block）、元素（element）、修饰符（modifier）, 是由Yandex团队提出的一种前端命名方法论。
>
> * `.block` 代表了更高级别的抽象或组件。
> * `.block__element` 代表.block的后代，用于形成一个完整的.block的整体。
> * `.block--modifier`代表.block的不同状态或不同版本。

![css-架构-bem-示意图](/Users/qxzm/Documents/GitHub/reading-notes/css/img/css-架构-bem-示意图.jpg)



#### 实践

1. **当遇到孙子或者更下级的选择器时**

   ```html
   <div class="c-card">
       <div class="c-card__header">
           <!-- Here comes the grandchild… -->
           <h2 class="c-card__header__title">Title text here</h2>
       </div>
       <div class="c-card__body">
   
           <img class="c-card__body__img" src="some-img.png" alt="description">
           <p class="c-card__body__text">
               Lorem ipsum dolor sit amet, consectetur
           </p>
           <p class="c-card__body__text">Adipiscing elit.
               <a href="/somelink.html" class="c-card__body__text__link">Pellentesque amet
               </a>
           </p>
   
       </div>
   </div>
   ```

   双下划线最好只出现一次，此处可修改为

   ```html
   <div class="c-card">
       <div class="c-card__header">
           <h2 class="c-card__title">Title text here</h2>
       </div>
   
       <div class="c-card__body">
   
           <img class="c-card__img" src="some-img.png" alt="description">
           <p class="c-card__text">Lorem ipsum dolor sit amet, consectetur</p>
           <p class="c-card__text">Adipiscing elit.
               <a href="/somelink.html" class="c-card__link">Pellentesque amet</a>
           </p>
   
       </div>
   </div>
   ```

   

2. **命名空间的使用**

   ​	类似下方的前缀，可以提高可读性（qa-可以来表示 qa测试，ss- 来和服务器挂钩）![css-架构-bem-命名空间](/Users/qxzm/Documents/GitHub/reading-notes/css/img/css-架构-bem-命名空间.png)

3. **跨组件，一个组件的样式和布局可能会收到其父组件的影响**

   ```html
   <div class="c-card">
       <div class="c-card__header">
           <h2 class="c-card__title">Title text here</h3>
       </div>
   
       <div class="c-card__body">
   
           <img class="c-card__img" src="some-img.png">
           <p class="c-card__text">Lorem ipsum dolor sit amet, consectetur</p>
           <p class="c-card__text">Adipiscing elit. Pellentesque.</p>
   
           <!-- here -->
           <button class="c-button c-button--primary">Click me!</button>
   
       </div>
   </div>
   ```

   这里的button是标准样式，如果在card里的button需要有圆角或者其他的不同，以前的做法可能是加一个.c-card__c-button 类

   真正模块化的UI元素的修饰不应该去关心元素的父容器，应该是

   ```html
   <button class="c-button c-button--rounded c-button--small">Click me!</button>
   ```

4. **添加修饰符还是新建一个组件**

   在c-card例子里面，你可能还会创建一个c-panel具有非常相似的样式属性，但也有一些明显的差异。我们尽量先考虑使用修饰符。如果发现css难以管理的时候就是放弃修饰符的时候，重开一个组件

5. **组件该不该有多个类**

   多个类的语法虽然不是最好看，但是明确