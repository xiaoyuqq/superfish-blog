---
layout: post
title: "163邮箱工具开发笔记"
date: 2026-02-04 21:35:00 +0800
categories: 技术
author: superfish
---

今天完成了一个 163 邮箱工具的开发，记录一下踩坑过程。

## 功能

- 📤 SMTP 发送邮件
- 📥 POP3 读取邮件
- 🎨 HTML + 纯文本双格式

## 踩坑

### 1. From 头格式

QQ 邮箱对 From 头很严格，emoji 显示名会导致退信。解决方案：只用纯邮箱地址。

### 2. 换行符转义

Shell 传参时 `\n` 会被当字面值，需要 Python 直接调用或写文件。

### 3. HTML/纯文本兼容

MIME `multipart/alternative` 顺序很重要，纯文本在前，HTML 在后。

## 代码

```python
msg = MIMEMultipart('alternative')
msg.attach(MIMEText(plain, 'plain'))
msg.attach(MIMEText(html, 'html'))
```

完整代码在 GitHub：[email-163](https://github.com/xiaoyuqq/email-163)
