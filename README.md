# 昙花科技官网（GitHub Pages）

北京昙花永现科技有限公司静态官网，域名：**tanhuatech.top**

## 本地预览

```bash
cd tanhua-website
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

## 部署到 GitHub Pages（完整步骤）

### 1. 创建 GitHub 仓库

1. 登录 [GitHub](https://github.com)
2. 点击 **New repository**
3. 仓库名建议：`tanhua-website`（或任意名称）
4. 选择 **Public**（免费 Pages 需要公开仓库，或使用 GitHub Pro 的私有仓库 Pages）
5. 不要勾选「Add a README」（本地已有代码时）
6. 创建仓库

### 2. 推送代码

将 `YOUR_GITHUB_USERNAME` 替换为你的 GitHub 用户名：

```bash
cd /path/to/tanhua-website
git init
git add .
git commit -m "feat: 公司官网静态站点"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/tanhua-website.git
git push -u origin main
```

### 3. 开启 GitHub Pages

1. 打开仓库 → **Settings** → **Pages**
2. **Source** 选择 **Deploy from a branch**
3. **Branch** 选 `main`，文件夹选 **`/ (root)`**
4. 点击 **Save**
5. 等待 1～3 分钟，站点会先出现在：`https://YOUR_GITHUB_USERNAME.github.io/tanhua-website/`

> 若仓库名为 `YOUR_GITHUB_USERNAME.github.io`，则根路径即为主站，可跳过子路径问题。

**推荐（自定义域名更简单）：** 将仓库命名为 `tanhuatech.top` 或 `www.tanhuatech.top` 不现实；更常见做法是：
- 仓库名任意（如 `tanhua-website`）
- 在 Pages 设置里填写自定义域名 `tanhuatech.top`
- 根目录的 `CNAME` 文件已包含 `tanhuatech.top`

### 4. 配置自定义域名（GitHub 侧）

1. 仓库 **Settings** → **Pages**
2. **Custom domain** 填入：`tanhuatech.top`
3. 勾选 **Enforce HTTPS**（DNS 生效且证书签发后可选）
4. GitHub 会自动在仓库保留/更新 `CNAME` 文件

### 5. 阿里云 DNS 解析

登录 [阿里云域名控制台](https://dc.console.aliyun.com/) → 找到 `tanhuatech.top` → **解析设置**：

#### 方案 A：根域名 `tanhuatech.top`（推荐，与 CNAME 文件一致）

添加 **A 记录**（4 条，主机记录均为 `@`）：

| 记录类型 | 主机记录 | 记录值 |
|---------|---------|--------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

可选：添加 **AAAA** 记录（IPv6，4 条）：

| 记录类型 | 主机记录 | 记录值 |
|---------|---------|--------|
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

#### 方案 B：`www` 子域名

| 记录类型 | 主机记录 | 记录值 |
|---------|---------|--------|
| CNAME | www | YOUR_GITHUB_USERNAME.github.io |

若使用 `www`，需在 GitHub Pages 自定义域名填 `www.tanhuatech.top`，并修改仓库根目录 `CNAME` 文件内容。

#### 等待生效

- DNS 通常 **10 分钟～24 小时** 生效
- 回到 GitHub Pages 设置页，应显示 **DNS check successful**
- 证书就绪后开启 **Enforce HTTPS**

### 6. 验证

```bash
# 检查解析
dig tanhuatech.top +short

# 浏览器访问
open https://tanhuatech.top
open https://tanhuatech.top/privacy.html
```

## 申请苹果开发者账号（组织）要点

1. **网站可公开访问**，且显示与营业执照一致的**公司法定名称**（本站已包含）
2. 准备 **D-U-N-S 编号**（在 [Apple 开发者网站](https://developer.apple.com) 申请组织账号时按指引获取）
3. 使用 **公司域名邮箱**（如 `contact@tanhuatech.top`）更利于审核
4. 隐私政策 URL 可填写：`https://tanhuatech.top/privacy.html`
5. 确保网站有**联系方式**（邮箱、官网）

## 上线前请修改

- [ ] 将 `contact@tanhuatech.top` 在阿里云邮件推送/企业邮箱中配置为可收发
- [ ] 在 `index.html` 中补充真实**办公地址**（与营业执照一致更佳）
- [ ] 如需 ICP 备案，备案通过后在页脚添加备案号

## 费用说明

| 项目 | 费用 |
|------|------|
| GitHub Pages | 免费（公开仓库） |
| 域名续费 | 阿里云按年付费（你已购买） |
| 企业邮箱 | 可选，阿里云免费转发或付费邮箱 |
