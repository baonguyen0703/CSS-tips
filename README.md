# CSS-tips

## 1. [Effect] Background color slide in when hovering on button
**Solution**: create ::before element, apply translateX transition
```scss
// Template
.containter { 
  position: relative 
  overflow: hidden // ::before element won’t be visible outside container  
}
.container::before {
  position: absolute
  transform: translateX(100%)
  // background or background-color
  // z-index of other elements (text, icon) must higher than this element
}
.container:hover::before {
  transition: all 0.5s ease
  transform: translateX(0%)
} 
```
<details> 
  <summary>Sample code</summary>  
  
  ```scss
  // scss
  .main-btn {
      position: relative;
      border: 2px solid var(--color-secondary);
      border-radius: 2rem;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 1rem;
      overflow: hidden;
      .btn-text {
          margin-left: 2rem;
          z-index: 1;
      }
      .btn-icon {
          background-color: var(--color-secondary);
          display: flex;
          align-items: center;
          border-radius: 50%;
          padding: 1rem;
          margin-right: -1px;
          z-index: 1;
      }
      // slide-left effect on hover
      &::before {
          content: '';
          position: absolute;
          inset: -2px;
          border-radius: 2rem;
          background: linear-gradient(to left, var(--color-secondary), var(--color-variant-3));
          transform: translateX(100%);
      }
      &:hover::before {
          transition: all .5s ease;
          transform: translateX(0%);
      }
  }
  ```
</details>
<img src="https://github.com/baonguyen0703/CSS-tips/assets/98341055/d13317f6-d6ed-4677-83d0-74bc5757c6df" alt="" width='320px'></img>
