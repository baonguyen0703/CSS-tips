# CSS-tips

## 1. [Effect] Background color slides in when hovering on button
<img src="https://github.com/baonguyen0703/CSS-tips/assets/98341055/d13317f6-d6ed-4677-83d0-74bc5757c6df" alt="" width='320px'></img>

### Solution: 
- create **::before** element with **absolute** position
- **z-index** of the ::before element must be _lower_ than others elements in the same container
- apply **translate** on ::before element

#### Template:
```scss
// Template with key atrributes
.containter { 
  position: relative; 
  overflow: hidden; // ::before element won’t be visible outside container  
}

.container > * {
  z-index: 1; // front
}
.container::before {
  content: ''; // ::before element won't be added to the HTML without this attribute
  position: absolute;
  inset: 0; // same dimensions as the container
  transform: translateX(100%); // from_state
  z-index: 0; // back
  // background or background-color
}
.container:hover::before {
  transition: all 0.5s ease; // transition option
  transform: translateX(0%); // to_state
} 
```
<details> 
  <summary><h4>Sample code</h4></summary>  
  
  ```html
  // HTML
  <a href="" class="main-btn">
    <span class="btn-text">Download Resume</span>
    <span class="btn-icon"><i class="fa-solid fa-download"></i></span>
  </a>
  ```
  ```scss
  // SCSS
  .main-btn {
    position: relative;
    border: 2px solid var(--color-secondary);
    border-radius: 2rem;
    font-weight: 600;
    display: flex;
    align-items: center;
    gap: 1rem;
    overflow: hidden;

    * {
        z-index: 1;
    }

    .btn-text {
        margin-left: 2rem;
    }
    .btn-icon {
        background-color: var(--color-secondary);
        display: flex;
        align-items: center;
        border-radius: 50%;
        padding: 1rem;
        margin-right: -1px;
    }
    
    // effect: slide left on hover
    &::before {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: 2rem;
        background: linear-gradient(to left, var(--color-secondary), var(--color-variant-3));
        transform: translateX(100%);
        z-index: 0;
    }
    &:hover::before {
        transition: all .5s ease;
        transform: translateX(0%);
    }
    
  }
  ```
</details>
