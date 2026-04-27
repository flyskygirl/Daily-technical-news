# 📚 详细配置指南

## 🎯 目标

本指南将帮助你完成以下配置:
1. 获取 NewsAPI Key
2. 配置邮箱（SMTP）
3. 添加 GitHub Secrets
4. 测试并验证

**预计时间: 5-10 分钟**

---

## 第 1 步：获取 NewsAPI Key

### 注册 NewsAPI 账户

1. 访问 [NewsAPI.org](https://newsapi.org)
2. 点击右上角 **Register** 按钮
3. 填写注册信息:
   - Email
   - Password (至少 8 个字符)
   - Name

4. 验证邮箱 (查收邮件，点击验证链接)

### 获取 API Key

1. 登录 NewsAPI 账户
2. 点击右上角头像 → **Dashboard**
3. 在 **API Keys** 栏目可以看到你的 key
4. 复制这个 32 位的 key (例如: `a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`)

✅ **完成!** 你已经获得了 API Key

**免费版限制**: 每月 100 个请求 (在 100,000 请求的 NewsAPI 免费层中)

---

## 第 2 步：配置邮箱

根据你使用的邮箱类型选择对应的配置方式:

### 📧 Gmail 配置

#### 2.1 开启 2 步验证 (如果还没有)

1. 访问 [myaccount.google.com/security](https://myaccount.google.com/security)
2. 在左侧菜单找到 **2-Step Verification** (两步验证)
3. 点击 **Get Started**，按步骤完成

#### 2.2 生成应用密码

1. 访问 [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)
2. 选择:
   - **Select the app**: Mail
   - **Select the device**: Windows Computer (或你使用的设备类型)
3. 点击 **Generate**
4. Google 会生成一个 16 位的密码 (例如: `abcd efgh ijkl mnop`)
5. **复制这个密码** (不要有空格)

**Gmail 设置:**
```
SMTP_SERVER = smtp.gmail.com
SMTP_PORT = 465
SMTP_EMAIL = 你的Gmail邮箱 (例如: example@gmail.com)
SMTP_PASSWORD = 生成的应用密码 (16个字符，没有空格)
RECIPIENT_EMAIL = 接收邮件的邮箱 (通常与SMTP_EMAIL相同)
```

---

### 📧 QQ 邮箱配置

#### 2.1 获取授权码

1. 访问 [mail.qq.com](https://mail.qq.com)，使用 QQ 号和密码登录
2. 点击左上角 **设置** → **账户**
3. 找到 **POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务** 栏目
4. 点击 **生成授权码**
5. 按照提示验证身份 (通过 QQ 号或绑定的手机)
6. **保存生成的授权码** (16 位，例如: `abcdefghijklmnop`)

**QQ 邮箱设置:**
```
SMTP_SERVER = smtp.qq.com
SMTP_PORT = 465
SMTP_EMAIL = 你的QQ邮箱 (例如: 123456789@qq.com)
SMTP_PASSWORD = 生成的授权码
RECIPIENT_EMAIL = 接收邮件的邮箱
```

---

### 📧 Outlook / Hotmail 配置

**SMTP 设置:**
```
SMTP_SERVER = smtp-mail.outlook.com
SMTP_PORT = 587
SMTP_EMAIL = 你的 Outlook 邮箱
SMTP_PASSWORD = 你的邮箱密码
RECIPIENT_EMAIL = 接收邮件的邮箱
```

**注意**: Outlook 某些情况下需要在 Account Security 中允许第三方应用访问。

---

### 📧 其他邮箱配置

| 邮箱类型 | SMTP 服务器 | 端口 |
|---------|-----------|------|
| 163 邮箱 | smtp.163.com | 465 |
| 126 邮箱 | smtp.126.com | 465 |
| Yahoo | smtp.mail.yahoo.com | 465 |
| ProtonMail* | smtp.protonmail.ch | 465 |

*ProtonMail 需要配置应用密码，访问 [account.protonmail.com/security](https://account.protonmail.com/security)

---

## 第 3 步：添加 GitHub Secrets

### 访问 Secrets 页面

1. 打开你的仓库
2. 点击 **Settings** (设置标签页)
3. 在左侧菜单找到 **Secrets and variables** → **Actions**
4. 点击 **New repository secret** 按钮

### 添加 6 个 Secrets

按照以下顺序添加每个 Secret:

#### Secret 1: NEWSAPI_KEY
```
Name: NEWSAPI_KEY
Secret: [粘贴你从 NewsAPI 复制的 API Key]
```
点击 **Add secret**

#### Secret 2: SMTP_SERVER
```
Name: SMTP_SERVER
Secret: smtp.gmail.com (或你的邮箱 SMTP 服务器)
```
点击 **Add secret**

#### Secret 3: SMTP_PORT
```
Name: SMTP_PORT
Secret: 465
```
点击 **Add secret**

#### Secret 4: SMTP_EMAIL
```
Name: SMTP_EMAIL
Secret: [你的邮箱地址，例如: example@gmail.com]
```
点击 **Add secret**

#### Secret 5: SMTP_PASSWORD
```
Name: SMTP_PASSWORD
Secret: [生成的应用密码或授权码]
```
点击 **Add secret**

#### Secret 6: RECIPIENT_EMAIL
```
Name: RECIPIENT_EMAIL
Secret: [接收邮件的邮箱地址]
```
点击 **Add secret**

✅ **完成!** 所有 6 个 Secrets 已添加

### 验证 Secrets

添加完成后，你应该在 **Actions secrets and variables** 中看到这 6 个 secret:
- NEWSAPI_KEY
- SMTP_SERVER
- SMTP_PORT
- SMTP_EMAIL
- SMTP_PASSWORD
- RECIPIENT_EMAIL

---

## 第 4 步：测试

### 手动运行工作流

1. 打开仓库的 **Actions** 选项卡
2. 在左侧看到 **Daily Tech News** 工作流
3. 点击它，然后点击 **Run workflow** 按钮
4. 选择 **Run workflow** 执行一次测试运行

### 等待完成

1. 工作流开始运行，你会看到一个黄色/绿色的进度指示
2. 通常需要 2-3 分钟完成
3. 当状态变为绿色 ✅ 时表示成功

### 检查邮件

1. 打开你的接收邮箱
2. 查看是否收到了来自 SMTP_EMAIL 的邮件
3. 邮件标题应该是: "Global Daily Tech News - 2026-04-27"

### 查看日志

如果没有收到邮件，检查执行日志:

1. 点击最近的工作流运行
2. 点击 **Collect news and send email** job
3. 展开各个步骤查看日志输出
4. 查找 ❌ 错误信息

---

## 🔧 常见问题

### Q1: 收不到邮件

**检查清单:**

- [ ] 所有 6 个 Secrets 都正确添加了吗?
- [ ] SMTP_EMAIL 和 SMTP_PASSWORD 正确匹配吗?
- [ ] SMTP_SERVER 和 SMTP_PORT 正确吗?
- [ ] Gmail 用户: 是否生成了应用密码而不是使用账户密码?
- [ ] QQ 用户: 是否生成了授权码?
- [ ] 邮件是否在垃圾/垃圾邮件文件夹?
- [ ] 邮箱是否开启了 IMAP/SMTP?

**解决方案:**

1. 在 Actions 中手动运行工作流看是否有错误日志
2. 重新检查邮箱配置 (特别是 SMTP 密码)
3. 对于 Gmail: 查看 [Security settings](https://myaccount.google.com/lesssecureapps) (允许不太安全的应用)
4. 尝试使用一个新的测试邮箱

---

### Q2: Actions 工作流报错

**常见错误:**

- **SMTPAuthenticationError**: 密码不正确或使用了错误的密码类型
- **SMTPServerClosed**: SMTP 服务器地址或端口不正确
- **ConnectionRefusedError**: 防火墙阻止了连接

**解决:**

1. 再次验证所有 Secrets 的准确性
2. 使用正确的应用密码 (Gmail) 或授权码 (QQ)
3. 测试在本地电脑上使用这些凭据能否连接

---

### Q3: 修改运行时间

编辑 `.github/workflows/daily-news.yml`:

```yaml
schedule:
  - cron: '0 1 * * *'  # 改成你想要的时间
```

**时间对照表** (Cron 格式: 分 小时 日 月 周):

```
0 1 * * *   →  UTC 01:00  →  北京时间 09:00 (早上)
0 8 * * *   →  UTC 08:00  →  北京时间 16:00 (下午)
0 23 * * *  →  UTC 23:00  →  北京时间 07:00 (次日早)
30 6 * * *  →  UTC 06:30  →  北京时间 14:30
```

使用 [crontab.guru](https://crontab.guru) 在线生成你的 cron 表达式。

---

### Q4: 修改新闻数量

编辑 `scripts/collect_news.py`:

```python
NEWS_COUNT = 20  # 改成你想要的数量 (建议 10-50)
```

---

### Q5: 修改新闻来源和关键词

编辑 `scripts/collect_news.py`:

```python
params = {
    'q': 'technology OR AI OR machine learning',  # 改成你感兴趣的关键词
    'sortBy': 'publishedAt',
    'language': 'en',  # 'zh' 中文, 'en' 英文
    'pageSize': NEWS_COUNT,
    'apiKey': API_KEY
}
```

---

## ⚡ 进阶配置

### 1. 添加多个接收人

修改 `scripts/collect_news.py` 中的邮件发送部分:

```python
# 在 send_email 函数中修改
msg['To'] = ','.join([RECIPIENT_EMAIL, 'another@example.com'])

# 或者在 Secrets 中使用逗号分隔的邮箱列表
recipients = RECIPIENT_EMAIL.split(',')
for recipient in recipients:
    # 逐个发送
```

### 2. 自定义邮件样式

修改 `scripts/collect_news.py` 中的 `generate_html_email()` 函数来改变:
- 颜色 (现在是紫色渐变)
- 字体和大小
- 布局和间距

### 3. 集成 Slack 通知

在工作流文件中添加:

```yaml
- name: Send Slack notification
  uses: slackapi/slack-github-action@v1
  with:
    webhook-url: ${{ secrets.SLACK_WEBHOOK }}
    payload: |
      {
        "text": "Daily Tech News has been sent!"
      }
```

---

## 📞 需要帮助?

- 📖 查看 [README.md](README.md)
- 🐛 在 GitHub Issues 中报告问题
- 💬 GitHub Discussions 讨论

---

## ✅ 配置完成检查表

- [ ] 获得了 NewsAPI Key
- [ ] 配置了邮箱的 SMTP 设置
- [ ] 生成了应用密码或授权码
- [ ] 添加了 6 个 GitHub Secrets
- [ ] 手动运行工作流进行测试
- [ ] 收到了测试邮件
- [ ] 修改了运行时间 (可选)
- [ ] 检查了邮件样式 (可选)

🎉 **恭喜!** 你已经完成了所有配置。明天早上你会收到第一份全球科技日报！

---

<div align="center">

**祝你享受每日全球科技资讯！** 📰🌍

如有任何问题，请参考本指南或 GitHub Issues

</div>
