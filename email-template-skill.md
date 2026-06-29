---
name: "email-template"
description: "制作钓鱼演练邮件模板（HTML 压缩包）的完整规范：涵盖邮件正文 email、钓鱼落地页 index、中招提示页 index2 三类页面，包括链接/二维码钓鱼、Outlook 兼容性、表单提交跳转、变量格式与文件命名规则。"
---

# 邮件钓鱼演练模板制作规范

## 概述
本 skill 用于指导制作钓鱼演练邮件模板（HTML 压缩包），涵盖邮件正文（email）、钓鱼落地页（index）、中招提示页（index2）三类页面，以及 Outlook 兼容性、变量格式、表单提交等注意事项。

---

## 一、压缩包整体结构

一个完整的钓鱼演练模板压缩包通常包含 **2~3 个 HTML 文件** + `images/` 文件夹：

| 文件 | 作用 | 是否必需 |
|------|------|----------|
| `email.html` | 邮件正文，引导用户点击/扫码 | 必需 |
| `index.html` | 钓鱼落地页（伪造的登录/提交页面） | 可选 |
| `index2.html` | 中招提示页（提交后告知用户已中招） | 必需 |

**命名规则：**
- 若有钓鱼落地页：落地页 = `index.html`，中招提示页 = `index2.html`
- 若**无**钓鱼落地页（如纯二维码/链接直接中招）：中招提示页直接命名为 `index.html`

```
压缩包/
├── email.html          # 邮件正文
├── index.html          # 钓鱼落地页（或中招提示页）
├── index2.html         # 中招提示页（有落地页时）
└── images/
    └── offlinecode.png # 二维码图片（二维码钓鱼时必需）
```

---

## 二、邮件正文（email.html）制作

### 1. 链接钓鱼类
- 文中需放置**空链接** `href="javascript:void(0)"`，防止用户误点后真实跳转（平台会接管真实重定向）。
- 模拟真实钓鱼链接的位置和样式，使其看起来像可点击的超链接。

**推荐 AI 提示词：**
```
我需要制作一个钓鱼演练邮件模板，按照参考图的形式与内容；模拟钓鱼链接的位置<a href="javascript:void(0)">后面的内容，输出html给我
```

### 2. 二维码钓鱼类
- 压缩包内必须有 `images/` 文件夹，内含 `offlinecode.png`（钓鱼二维码）。
- HTML 中引用：`<img src="images/offlinecode.png" />`

**推荐 AI 提示词：**
```
我需要制作一个钓鱼演练邮件模板，二维码的地址使用 img src="images/offlinecode.png"，按照参考图的形式与内容输出html给我
```

---

## 三、钓鱼落地页（index.html）制作

### 核心要求
- 页面需具备**表单提交动作**（伪造登录/密码输入框），并在提交后**跳转到中招提示页 `index2.html`**。
- input 框必须添加 `name` 属性，便于平台采集提交内容。

**推荐 AI 提示词：**
```
输出落地页html
```

### 表单与提交规范
- 表单 action 指向中招提示页，method 用 post：
```html
<form id="submitForm" action="index2.html" method="post">
  <input class="form-input" type="password" name="password" placeholder="请输入您的邮箱密码" required="">
  <input type="submit" value="登录">
</form>
```
- input 必须带 `name` 属性（如 `name="password"`、`name="username"`）。
- **使用 `<input type="submit">`** 提交，兼容性好，避免手机端拦截表单提交。
- **不要使用 `<base target="_blank">`** 标签，可能导致移动端拦截或新窗口异常。

### 关于空链接的区分（重要）
- **邮件正文（email.html）里的钓鱼链接** → 用空链接 `javascript:void(0)`（由平台接管重定向）。
- **落地页（index.html）的表单 action** → 指向 `index2.html`，需真实跳转到中招提示页，**不能用空链接**，否则提交后无法到达提示页。

---

## 四、中招提示页（index2.html / index.html）

- 用户提交表单（或扫码/点击链接）后展示的页面，告知已中招。
- 若有落地页，命名为 `index2.html`；若无落地页，命名为 `index.html`。
- 内容通常为安全提示文案，可使用与邮件一致的风格。

---

## 五、Outlook 兼容性注意事项

- Outlook 可能**不支持 CSS 渐变语法**（`linear-gradient`、`radial-gradient` 等），用纯色背景替代。
- 避免 CSS Grid、Flexbox，改用 `<table>` 布局。
- 避免 `background-image` 等可能被 Outlook 屏蔽的属性。
- 尽量使用内联样式，减少 `<style>` 依赖。
- 字体用系统默认栈：`font-family: Arial, Helvetica, sans-serif`。

---

## 六、模板变量格式

### 日期
```
{{Y}}年{{n}}月{{j}}日 17:00 前
{{datetime|+3 day |Y-m-d H:i:s}}
```

### 人名
```
尊敬的{{recipient_full_name}}：
```

---

## 七、图片资源规范

- 页面所需图片统一放入 `images/` 文件夹。
- HTML 中用相对路径引用：`<img src="images/xxx.png" />`
- 二维码图片固定命名 `offlinecode.png`。

---

## 八、文件交付规范

1. 交付物为包含 HTML 文件和 `images/` 文件夹的**压缩包**。
2. 文件结构清晰，路径层级不超过一层。
3. HTML 编码 UTF-8，添加 `<meta charset="UTF-8">`，确保中文不乱码。
4. 确认文件命名符合"有/无落地页"规则。
