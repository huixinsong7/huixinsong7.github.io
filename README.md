# huixin.plus

个人主页站点,基于 **GitHub Pages** 部署,自定义域名 `huixin.plus`。

## 技术栈

- 纯静态 HTML / CSS(无构建步骤)
- GitHub Pages 直接托管 `main` 分支

## 本地预览

任意一个静态服务器即可,例如:

```bash
# Python
python3 -m http.server 8000

# 或 Node
npx serve .
```

打开 http://localhost:8000 查看。

## 部署步骤

### 1. 推送代码到 GitHub

```bash
git init
git add .
git commit -m "init: huixin.plus site"
git branch -M main
git remote add origin git@github.com:<your-username>/<repo-name>.git
git push -u origin main
```

> 推荐仓库名为 `<your-username>.github.io`(用户主站点),也可以用任意仓库名作为项目站点。

### 2. 在 GitHub 仓库开启 Pages

`Settings → Pages`:

- **Source**: Deploy from a branch
- **Branch**: `main` / `(root)`
- **Custom domain**: `huixin.plus`
- ✅ **Enforce HTTPS**(等 SSL 证书签发后勾选)

### 3. 配置 DNS 解析

在你的域名服务商(Cloudflare / 阿里云 / DNSPod 等)添加:

**根域名 A 记录** —— 指向 GitHub Pages 的 4 个 IP:

| 类型 | 主机记录 | 记录值 |
|------|---------|----------------------|
| A    | @       | 185.199.108.153      |
| A    | @       | 185.199.109.153      |
| A    | @       | 185.199.110.153      |
| A    | @       | 185.199.111.153      |

**www 子域名 CNAME** —— 指向你的 GitHub Pages 域名:

| 类型  | 主机记录 | 记录值                       |
|-------|---------|------------------------------|
| CNAME | www     | `<your-username>.github.io.` |

> Cloudflare 用户:如果开启橙色云朵代理,需关闭"Always Use HTTPS"或正确配置 SSL 模式为 Full,否则会重定向循环。

### 4. 验证

- DNS 生效后访问 https://huixin.plus
- GitHub 自动签发 Let's Encrypt 证书(几分钟到 24 小时)
- 证书签发完成后回到 Settings → Pages 勾选 Enforce HTTPS

## 文件说明

| 文件         | 作用                                         |
|--------------|----------------------------------------------|
| `index.html` | 站点首页                                     |
| `CNAME`      | **关键**,告诉 GitHub Pages 绑定的自定义域名 |
| `README.md`  | 项目说明                                     |
| `.gitignore` | Git 忽略规则                                 |
