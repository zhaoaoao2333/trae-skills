# 组件库

> 常用组件的HTML结构、CSS样式和JS交互代码片段。
>
> **组件中不包含具体色值**，颜色、字体、间距使用CSS变量引用 `prototype-rules.md` 的Design Token。
>
> 组件分为：导航、列表、弹窗、状态、表单、按钮、其他 七大类。

---

## 一、导航组件

### 1. 顶部导航栏（基础版）

```html
<div class="nav-bar">
  <div class="nav-back" onclick="goBack()">
    <svg class="icon-24" viewBox="0 0 24 24"><path d="M15 18l-6-6 6-6"/></svg>
  </div>
  <div class="nav-title">页面标题</div>
  <div class="nav-right"></div>
</div>
```

```css
.nav-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 56px;
  padding: 0 var(--spacing-page);
  background: var(--color-bg-primary);
}
.nav-back, .nav-right {
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.nav-title {
  font-size: var(--font-title);
  font-weight: 600;
  color: var(--color-text-primary);
}
```

### 2. 顶部导航栏（扩展版）

```html
<div class="nav-bar">
  <div class="nav-back" onclick="goBack()">
    <svg class="icon-24" viewBox="0 0 24 24"><path d="M15 18l-6-6 6-6"/></svg>
  </div>
  <div class="nav-title">页面标题</div>
  <div class="nav-right">
    <span class="nav-icon" onclick="navTo('search')">
      <svg class="icon-24" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="M21 21l-4.35-4.35"/></svg>
    </span>
    <span class="nav-icon" onclick="showActionSheet()">
      <svg class="icon-24" viewBox="0 0 24 24"><circle cx="12" cy="5" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="12" cy="19" r="2"/></svg>
    </span>
  </div>
</div>
```

**小程序适配**：右侧不放置任何内容（胶囊按钮区禁止覆盖）。

### 3. 底部导航栏

```html
<div class="tab-bar">
  <div class="tab-item active" data-tab="home" onclick="switchTab('home')">
    <svg class="tab-icon" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/></svg>
    <div class="tab-label">首页</div>
  </div>
  <div class="tab-item" data-tab="category" onclick="switchTab('category')">
    <svg class="tab-icon" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>
    <div class="tab-label">分类</div>
  </div>
  <div class="tab-item" data-tab="cart" onclick="switchTab('cart')">
    <svg class="tab-icon" viewBox="0 0 24 24"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
    <div class="tab-label">购物车</div>
    <div class="tab-badge">3</div>
  </div>
  <div class="tab-item" data-tab="mine" onclick="switchTab('mine')">
    <svg class="tab-icon" viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
    <div class="tab-label">我的</div>
  </div>
</div>
```

```css
.tab-bar {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 56px;
  background: var(--color-bg-primary);
  border-top: 1px solid var(--color-border);
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 1000;
}
.tab-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex: 1;
  height: 100%;
  position: relative;
}
.tab-icon {
  width: 24px;
  height: 24px;
  stroke: var(--color-text-tertiary);
  fill: none;
  stroke-width: 2;
}
.tab-item.active .tab-icon {
  stroke: var(--color-primary);
}
.tab-label {
  font-size: 10px;
  color: var(--color-text-tertiary);
  margin-top: 2px;
}
.tab-item.active .tab-label {
  color: var(--color-primary);
}
.tab-badge {
  position: absolute;
  top: 2px;
  right: calc(50% - 16px);
  min-width: 16px;
  height: 16px;
  padding: 0 4px;
  background: var(--color-error);
  color: #fff;
  font-size: 10px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

---

## 二、列表组件

### 4. 纵向列表项（左图+右信息）

```html
<div class="list-item" onclick="navTo('detail')">
  <img class="item-img" src="placeholder.jpg">
  <div class="item-info">
    <div class="item-title">标题文字，最多两行截断</div>
    <div class="item-desc">描述文字，辅助信息</div>
    <div class="item-tags">
      <span class="tag">标签1</span>
      <span class="tag">标签2</span>
    </div>
    <div class="item-bottom">
      <span class="item-price">¥99</span>
      <span class="item-action">按钮</span>
    </div>
  </div>
</div>
```

```css
.list-item {
  display: flex;
  padding: var(--spacing-card);
  background: var(--color-bg-primary);
}
.item-img {
  width: 100px;
  height: 100px;
  border-radius: var(--radius-card);
  object-fit: cover;
  flex-shrink: 0;
}
.item-info {
  flex: 1;
  margin-left: var(--spacing-element);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-width: 0;
}
.item-title {
  font-size: var(--font-body);
  color: var(--color-text-primary);
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.item-desc {
  font-size: var(--font-caption);
  color: var(--color-text-secondary);
  margin-top: 4px;
}
.item-tags {
  margin-top: 4px;
}
.item-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 4px;
}
.item-price {
  font-size: var(--font-title);
  font-weight: bold;
  color: var(--color-primary);
}
```

### 5. 双列网格卡片

```html
<div class="grid-2col">
  <div class="grid-card" onclick="navTo('detail')">
    <img class="card-img" src="placeholder.jpg">
    <div class="card-title">商品标题</div>
    <div class="card-price">¥99</div>
  </div>
</div>
```

```css
.grid-2col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-element);
  padding: var(--spacing-page);
}
.grid-card {
  background: var(--color-bg-primary);
  border-radius: var(--radius-card);
  overflow: hidden;
}
.card-img {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
}
.card-title {
  font-size: var(--font-body);
  color: var(--color-text-primary);
  padding: 8px;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.card-price {
  font-size: var(--font-title);
  font-weight: bold;
  color: var(--color-primary);
  padding: 0 8px 8px;
}
```

### 6. 横向滚动卡片

```html
<div class="scroll-x">
  <div class="card-h" onclick="navTo('detail')">
    <img class="card-h-img" src="placeholder.jpg">
    <div class="card-h-title">标题</div>
    <div class="card-h-price">¥99</div>
  </div>
</div>
```

```css
.scroll-x {
  display: flex;
  overflow-x: auto;
  gap: var(--spacing-element);
  padding: 0 var(--spacing-page);
  scrollbar-width: none;
}
.scroll-x::-webkit-scrollbar {
  display: none;
}
.card-h {
  flex-shrink: 0;
  width: 140px;
  background: var(--color-bg-primary);
  border-radius: var(--radius-card);
  overflow: hidden;
}
.card-h-img {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
}
.card-h-title {
  font-size: var(--font-caption);
  color: var(--color-text-primary);
  padding: 8px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.card-h-price {
  font-size: var(--font-body);
  font-weight: bold;
  color: var(--color-primary);
  padding: 0 8px 8px;
}
```

---

## 三、弹窗组件

### 7. 中部确认弹窗

```html
<div class="modal-overlay" id="confirmModal" onclick="closeModal()">
  <div class="modal-box" onclick="event.stopPropagation()">
    <div class="modal-title">确认删除？</div>
    <div class="modal-content">删除后不可恢复</div>
    <div class="modal-btns">
      <button class="btn-secondary" onclick="closeModal()">取消</button>
      <button class="btn-primary" onclick="confirmDelete()">删除</button>
    </div>
  </div>
</div>
```

```css
.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0,0,0,0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
}
.modal-box {
  width: 300px;
  background: var(--color-bg-primary);
  border-radius: var(--radius-modal);
  padding: var(--spacing-module);
  text-align: center;
}
.modal-title {
  font-size: var(--font-title);
  font-weight: 600;
  color: var(--color-text-primary);
}
.modal-content {
  font-size: var(--font-body);
  color: var(--color-text-secondary);
  margin-top: var(--spacing-element);
}
.modal-btns {
  display: flex;
  gap: var(--spacing-element);
  margin-top: var(--spacing-module);
}
```

### 8. 底部弹窗

```html
<div class="modal-overlay" id="bottomModal" onclick="closeBottomModal()">
  <div class="modal-bottom" onclick="event.stopPropagation()">
    <div class="modal-bottom-header">
      <span class="modal-close" onclick="closeBottomModal()">✕</span>
      <span class="modal-bottom-title">选择规格</span>
    </div>
    <div class="modal-bottom-body">
      <!-- 内容 -->
    </div>
    <div class="modal-bottom-footer">
      <button class="btn-primary btn-full">确定</button>
    </div>
  </div>
</div>
```

```css
.modal-bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--color-bg-primary);
  border-radius: var(--radius-modal) var(--radius-modal) 0 0;
  max-height: 50vh;
  display: flex;
  flex-direction: column;
  z-index: 2100;
}
.modal-bottom-header {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 48px;
  border-bottom: 1px solid var(--color-border);
  position: relative;
}
.modal-close {
  position: absolute;
  left: var(--spacing-page);
  font-size: 20px;
  color: var(--color-text-secondary);
}
.modal-bottom-title {
  font-size: var(--font-title);
  font-weight: 600;
}
.modal-bottom-body {
  flex: 1;
  overflow-y: auto;
  padding: var(--spacing-module);
}
.modal-bottom-footer {
  padding: var(--spacing-page);
  border-top: 1px solid var(--color-border);
}
```

### 9. ActionSheet

```html
<div class="modal-overlay" id="actionSheet" onclick="closeActionSheet()">
  <div class="action-sheet" onclick="event.stopPropagation()">
    <div class="action-sheet-item" onclick="doAction('edit')">编辑</div>
    <div class="action-sheet-item" onclick="doAction('delete')">删除</div>
    <div class="action-sheet-item" onclick="doAction('share')">分享</div>
    <div class="action-sheet-cancel" onclick="closeActionSheet()">取消</div>
  </div>
</div>
```

```css
.action-sheet {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--color-bg-primary);
  border-radius: var(--radius-modal) var(--radius-modal) 0 0;
  z-index: 2100;
}
.action-sheet-item {
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--font-body);
  color: var(--color-text-primary);
  border-bottom: 1px solid var(--color-border);
}
.action-sheet-cancel {
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--font-body);
  color: var(--color-text-secondary);
  margin-top: 8px;
  border-top: 1px solid var(--color-border);
}
```

---

## 四、状态组件

### 10. 骨架屏

```html
<div class="skeleton">
  <div class="skeleton-line" style="width: 60%"></div>
  <div class="skeleton-line" style="width: 80%"></div>
  <div class="skeleton-line" style="width: 40%"></div>
</div>
```

```css
.skeleton {
  padding: var(--spacing-card);
}
.skeleton-line {
  height: 16px;
  background: linear-gradient(90deg, var(--color-bg-tertiary) 25%, var(--color-bg-secondary) 50%, var(--color-bg-tertiary) 75%);
  background-size: 200% 100%;
  border-radius: 4px;
  margin-bottom: 8px;
  animation: skeleton-loading 1.5s infinite;
}
@keyframes skeleton-loading {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### 11. 空状态

```html
<div class="empty-state">
  <div class="empty-icon">📭</div>
  <div class="empty-text">暂无数据</div>
  <div class="empty-desc">去添加一些内容吧</div>
  <button class="btn-primary" onclick="navTo('create')">去添加</button>
</div>
```

```css
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-module) var(--spacing-page);
  min-height: 300px;
}
.empty-icon {
  font-size: 64px;
  margin-bottom: var(--spacing-element);
}
.empty-text {
  font-size: var(--font-title);
  color: var(--color-text-primary);
  font-weight: 600;
}
.empty-desc {
  font-size: var(--font-body);
  color: var(--color-text-secondary);
  margin-top: 4px;
}
.empty-state .btn-primary {
  margin-top: var(--spacing-module);
}
```

### 12. Toast

```javascript
function showToast(message, duration = 2000) {
  const toast = document.createElement('div');
  toast.className = 'toast';
  toast.textContent = message;
  document.body.appendChild(toast);
  
  // 动画进入
  toast.style.opacity = '0';
  toast.style.transform = 'translate(-50%, 20px)';
  setTimeout(() => {
    toast.style.opacity = '1';
    toast.style.transform = 'translate(-50%, 0)';
  }, 10);
  
  // 自动消失
  setTimeout(() => {
    toast.style.opacity = '0';
    toast.style.transform = 'translate(-50%, -20px)';
    setTimeout(() => toast.remove(), 300);
  }, duration);
}
```

```css
.toast {
  position: absolute;
  bottom: 100px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0,0,0,0.8);
  color: #fff;
  padding: 10px 20px;
  border-radius: 20px;
  font-size: var(--font-body);
  z-index: 3000;
  transition: all 0.3s ease;
}
```

---

## 五、表单组件

### 13. 输入框

```html
<div class="form-item">
  <label class="form-label">手机号 <span class="required">*</span></label>
  <input class="form-input" type="tel" placeholder="请输入手机号" maxlength="11">
  <div class="form-error">手机号格式错误</div>
</div>
```

```css
.form-item {
  margin-bottom: var(--spacing-module);
}
.form-label {
  display: block;
  font-size: var(--font-body);
  color: var(--color-text-primary);
  margin-bottom: 8px;
}
.required {
  color: var(--color-error);
}
.form-input {
  width: 100%;
  height: 44px;
  padding: 0 12px;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-input);
  font-size: var(--font-body);
  color: var(--color-text-primary);
  background: var(--color-bg-primary);
}
.form-input:focus {
  border-color: var(--color-primary);
  outline: none;
}
.form-error {
  font-size: var(--font-caption);
  color: var(--color-error);
  margin-top: 4px;
  display: none;
}
.form-item.error .form-error {
  display: block;
}
.form-item.error .form-input {
  border-color: var(--color-error);
}
```

### 14. 搜索框

```html
<div class="search-bar">
  <div class="search-input-wrap">
    <svg class="search-icon" viewBox="0 0 24 24"><circle cx="11" cy="11" r="8"/><path d="M21 21l-4.35-4.35"/></svg>
    <input class="search-input" placeholder="搜索商品/门店/内容">
    <span class="search-clear" onclick="clearSearch()">✕</span>
  </div>
  <button class="search-btn" onclick="doSearch()">搜索</button>
</div>
```

```css
.search-bar {
  display: flex;
  align-items: center;
  gap: var(--spacing-element);
  padding: var(--spacing-page);
}
.search-input-wrap {
  flex: 1;
  display: flex;
  align-items: center;
  height: 40px;
  background: var(--color-bg-tertiary);
  border-radius: 20px;
  padding: 0 12px;
}
.search-icon {
  width: 20px;
  height: 20px;
  stroke: var(--color-text-tertiary);
  fill: none;
  stroke-width: 2;
  flex-shrink: 0;
}
.search-input {
  flex: 1;
  border: none;
  background: transparent;
  font-size: var(--font-body);
  margin: 0 8px;
  outline: none;
}
.search-clear {
  font-size: 16px;
  color: var(--color-text-tertiary);
  display: none;
}
.search-input:not(:placeholder-shown) + .search-clear {
  display: block;
}
.search-btn {
  font-size: var(--font-body);
  color: var(--color-primary);
  background: none;
  border: none;
}
```

---

## 六、按钮组件

### 15. 主按钮

```html
<button class="btn-primary">主要操作</button>
```

```css
.btn-primary {
  height: 44px;
  padding: 0 var(--spacing-module);
  background: var(--color-primary);
  color: #fff;
  font-size: var(--font-body);
  font-weight: 600;
  border: none;
  border-radius: var(--radius-button);
  width: 100%;
}
.btn-primary:active {
  transform: scale(0.95);
  opacity: 0.9;
}
.btn-primary:disabled {
  background: var(--color-bg-tertiary);
  color: var(--color-text-tertiary);
}
```

### 16. 次按钮

```html
<button class="btn-secondary">次要操作</button>
```

```css
.btn-secondary {
  height: 44px;
  padding: 0 var(--spacing-module);
  background: transparent;
  color: var(--color-primary);
  font-size: var(--font-body);
  font-weight: 600;
  border: 1px solid var(--color-primary);
  border-radius: var(--radius-button);
  width: 100%;
}
.btn-secondary:active {
  background: rgba(var(--color-primary-rgb), 0.1);
}
```

### 17. 图标按钮

```html
<button class="btn-icon" onclick="doAction()">
  <svg class="icon-24" viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
  <span class="btn-icon-label">收藏</span>
</button>
```

```css
.btn-icon {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  background: none;
  border: none;
  padding: 8px;
}
.btn-icon .icon-24 {
  stroke: var(--color-text-secondary);
  fill: none;
  stroke-width: 2;
}
.btn-icon.active .icon-24 {
  fill: var(--color-primary);
  stroke: var(--color-primary);
}
.btn-icon-label {
  font-size: 10px;
  color: var(--color-text-secondary);
}
```

---

## 七、其他组件

### 18. 标签

```html
<span class="tag tag-primary">促销</span>
<span class="tag tag-secondary">新品</span>
<span class="tag tag-outline">标签</span>
```

```css
.tag {
  display: inline-block;
  padding: 2px 6px;
  font-size: 10px;
  border-radius: 4px;
  margin-right: 4px;
}
.tag-primary {
  background: var(--color-primary);
  color: #fff;
}
.tag-secondary {
  background: rgba(var(--color-primary-rgb), 0.1);
  color: var(--color-primary);
}
.tag-outline {
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
}
```

### 19. 评分星星

```html
<div class="rating">
  <svg class="star filled" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
  <svg class="star filled" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
  <svg class="star filled" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
  <svg class="star filled" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
  <svg class="star" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
  <span class="rating-score">4.5</span>
</div>
```

```css
.rating {
  display: flex;
  align-items: center;
  gap: 2px;
}
.star {
  width: 16px;
  height: 16px;
  fill: var(--color-bg-tertiary);
  stroke: var(--color-bg-tertiary);
  stroke-width: 1;
}
.star.filled {
  fill: #FFB800;
  stroke: #FFB800;
}
.rating-score {
  font-size: var(--font-caption);
  color: var(--color-text-secondary);
  margin-left: 4px;
}
```

### 20. 轮播图

```html
<div class="swiper" id="swiper1">
  <div class="swiper-wrap">
    <img class="swiper-item" src="banner1.jpg">
    <img class="swiper-item" src="banner2.jpg">
    <img class="swiper-item" src="banner3.jpg">
  </div>
  <div class="swiper-dots">
    <span class="dot active"></span>
    <span class="dot"></span>
    <span class="dot"></span>
  </div>
</div>
```

```css
.swiper {
  position: relative;
  overflow: hidden;
  border-radius: var(--radius-card);
}
.swiper-wrap {
  display: flex;
  transition: transform 0.3s ease;
}
.swiper-item {
  width: 100%;
  flex-shrink: 0;
  aspect-ratio: 16/9;
  object-fit: cover;
}
.swiper-dots {
  position: absolute;
  bottom: 8px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 6px;
}
.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: rgba(255,255,255,0.5);
}
.dot.active {
  background: #fff;
  width: 12px;
  border-radius: 3px;
}
```

```javascript
// 简单轮播逻辑
function initSwiper(id, interval = 5000) {
  const swiper = document.getElementById(id);
  const wrap = swiper.querySelector('.swiper-wrap');
  const dots = swiper.querySelectorAll('.dot');
  let current = 0;
  const total = dots.length;
  
  function goTo(index) {
    wrap.style.transform = `translateX(-${index * 100}%)`;
    dots.forEach((d, i) => d.classList.toggle('active', i === index));
    current = index;
  }
  
  setInterval(() => goTo((current + 1) % total), interval);
}
```

---

## 组件使用说明

### 引用方式

1. **复制组件代码**到页面HTML中
2. **确保CSS变量已定义**（在 `:root` 或页面 `<style>` 中）
3. **替换占位内容**为实际业务数据
4. **绑定事件处理函数**

### CSS变量要求

组件依赖以下CSS变量，必须在页面中定义。变量名必须与 `prototype-rules.md` 第七章统一设计Token完全一致：

```css
:root {
  /* 品牌色 */
  --color-primary: #FF6B35;
  --color-primary-light: #FF8A5C;
  --color-primary-dark: #E55A2B;
  
  /* 功能色 */
  --color-success: #52c41a;
  --color-warning: #faad14;
  --color-error: #ff4d4f;
  
  /* 文字色 */
  --color-text-primary: #333333;
  --color-text-secondary: #666666;
  --color-text-tertiary: #999999;
  
  /* 背景色 */
  --color-bg-primary: #ffffff;
  --color-bg-secondary: #f5f5f5;
  --color-bg-tertiary: #f0f0f0;
  
  /* 边框与分割 */
  --color-border: #e5e5e5;
  --color-divider: #f0f0f0;
  
  /* 字体 */
  --font-h1: 20px;
  --font-h2: 16px;
  --font-title: 16px;
  --font-body: 14px;
  --font-caption: 12px;
  
  /* 间距（基于8px网格） */
  --spacing-page: 16px;
  --spacing-module: 16px;
  --spacing-card: 12px;
  --spacing-element: 8px;
  --spacing-compact: 4px;
  
  /* 圆角 */
  --radius-card: 12px;
  --radius-button: 6px;
  --radius-input: 8px;
  --radius-modal: 16px;
}
```
