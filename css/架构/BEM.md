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

3. 