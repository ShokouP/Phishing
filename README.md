# Phishing Simulation Templates

钓鱼演练邮件模板制作规范与工具集。

## 文件说明

- **[email-template-skill.md](email-template-skill.md)** — 邮件钓鱼演练模板制作 Skill，包含完整的提示词规范、Outlook 兼容性注意事项、变量格式和文件交付标准。

## 快速使用

将 `email-template-skill.md` 的内容导入为 Claude/Cowork 的 Skill，即可在任意会话中自动加载钓鱼邮件模板制作规范。

## 制作场景

- **链接钓鱼** — 文中嵌入空链接 `href="javascript:void(0)"` 模拟钓鱼行为
- **二维码钓鱼** — 使用 `images/offlinecode.png` 引导扫码

## 兼容性

- 针对 Outlook 客户端做了适配（避免 CSS 渐变、使用 table 布局）
- UTF-8 编码，支持中文

## 变量格式

| 类型 | 示例 |
|------|------|
| 日期 | `{{Y}}年{{n}}月{{j}}日 17:00 前` |
| 日期偏移 | `{{datetime\|+3 day \|Y-m-d H:i:s}}` |
| 人名 | `{{recipient_full_name}}` |
