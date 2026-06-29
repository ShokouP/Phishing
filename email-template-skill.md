---
name: "email-template"
description: "制作钓鱼演练邮件模板（HTML）的规范与提示词，涵盖链接钓鱼、二维码钓鱼、Outlook 兼容性及变量格式。"
---

# 邮件钓鱼演练模板制作规范

## 概述
本 skill 用于指导制作钓鱼演练邮件模板（HTML 格式），涵盖链接钓鱼和二维码钓鱼两种场景，以及 Outlook 兼容性、日期人名变量等注意事项。

---

## 一、链接钓鱼类模板

### 核心要点
- 文中需放置**空链接**，即 `href="javascript:void(0)"`，防止用户误点后跳转。
- 模拟真实钓鱼链接的位置和样式，使其看起来像可点击的超链接。

### 推荐 AI 提示词
```
我需要制作一个钓鱼演练邮件模板，按照参考图的形式与内容；模拟钓鱼链接的位置<a href="javascript:void(0)">后面的内容，输出html给我
```

---

## 二、二维码钓鱼类模板

### 文件结构要求
压缩包内必须包含以下结构：
```
├── email.html          # 邮件模板 HTML
└── images/
    └── offlinecode.png  # 钓鱼二维码图片
```

### 图片引用方式
```html
<img src="images/offlinecode.png" />
```

### 推荐 AI 提示词
```
我需要制作一个钓鱼演练邮件模板，二维码的地址使用 img src="images/offlinecode.png"，按照参考图的形式与内容输出html给我
```

---

## 三、Outlook 兼容性注意事项

- Outlook 可能**不支持 CSS 渐变语法**（如 `linear-gradient`、`radial-gradient` 等），应使用纯色背景替代。
- 避免使用 CSS Grid、Flexbox 等现代布局，改用 `<table>` 布局以确保兼容性。
- 避免使用 `background-image` 等可能被 Outlook 屏蔽的属性。
- 尽量使用内联样式，减少 `<style>` 标签中的样式依赖。
- 字体使用系统默认字体栈（如 `font-family: Arial, Helvetica, sans-serif`）。

---

## 四、模板变量格式

### 日期格式
```
{{Y}}年{{n}}月{{j}}日 17:00 前
{{datetime|+3 day |Y-m-d H:i:s}}
```

### 人名格式
```
尊敬的{{recipient_full_name}}：
```

---

## 五、图片资源规范

- 页面所需的图片统一放入 `images/` 文件夹。
- HTML 中引用图片时使用**相对路径**：
```html
<img src="images/xxx.png" />
```
- 注意：Markdown/纯文本中展示代码时，`<img` 与 `src` 之间需有空格，但实际 HTML 中应写为 `<img src="images/xxx.png" />`。

---

## 六、文件交付规范

1. 最终交付物为包含 HTML 文件和 `images/` 文件夹的**压缩包**。
2. 压缩包内文件结构清晰，路径层级不超过一层。
3. HTML 文件编码为 UTF-8，确保中文不乱码（添加 `<meta charset="UTF-8">`）。

