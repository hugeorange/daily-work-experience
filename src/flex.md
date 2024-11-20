1. 容器 div 分左右两栏，left、right 其中 left 宽度固定 right 宽度根据屏幕剩余宽度自动撑开
   - 当右边子元素内容超宽时，要求不挤压 left，不撑大 right
   ```html
   <div class="wrap">
    <div class="left">Left</div>
    <div class="right">
      <div>超宽元素</div>
    </div>
   </div>
   ```
   ```scss
    .wrap {
      display: flex;
      .left {
        width: 100px;
        flex-shink: 0; // 确保左边的固定宽度容器不会被压缩，即使右边的内容非常多。
      }
      .right {
        flex: 1; // 右边容器占据剩余空间
        min-width: 0; // 防止子元素撑开父容器
        /* 
          min-width: 0; 起作用的原因是:
          flex 布局中，子元素默认具有 min-width: auto;
          auto 会让子元素宽度至少等于其内容宽度，因此当子元素内容过宽时会导致其父容器被撑开，导致布局异常

          min-width: 0;
          右边容器被允许缩小到小于内容宽度
          取消子容器内容宽度的限制，使得父容器可以缩小，不受子元素宽度的影响
        **/
      }
    }
   ```