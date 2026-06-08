# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概览

`huixin.plus` 自定义域名的个人站点，通过 **GitHub Pages** 从 `main` 分支根目录直接部署。无构建步骤，仓库根目录的文件即是上线产物。`CNAME` 文件用于绑定自定义域名,任何改动都必须保留它。

## Language

使用简体中文进行对话和创建内容。

## 本地预览

无包管理器、无需安装。在仓库根目录启动任意静态服务器即可:

```bash
python3 -m http.server 8000
# 或
npx serve .
```

然后访问 <http://localhost:8000> 查看 `index.html`,或 <http://localhost:8000/lesson.html>。

## 部署

`git push origin main` 就是部署。GitHub Pages 直接托管该分支,没有 CI、没有构建产物。DNS 与 Pages 设置(自定义域名、Enforce HTTPS、A/CNAME 记录)详见 [README.md](README.md) —— 在改动 `CNAME` 或任何会影响路由的内容之前请先查阅。

## 代码结构

两个互相独立的单文件 HTML 页面,不共享任何资源,也未互相链接:

- [index.html](index.html) —— 站点落地页。完全自包含:内联 `<style>`、无外部脚本、SVG data-URI favicon,使用 CSS 自定义属性(`--bg`、`--fg`、`--accent`、`--muted`)实现的深色渐变主题。
- [lesson.html](lesson.html) —— 全屏移动端 H5 宣传册("即兴小玩家 · 课程体系魔法宣传册"),按纵向 scroll-snap 幻灯片形式呈现(`.slide-container` + `.slide-page`,配合 `scroll-snap-type: y mandatory`)。每一个顶层 `<section class="slide-page">` 就是一屏。通过 CDN 引入 **Tailwind CSS**(`cdn.tailwindcss.com`)与 **Lucide Icons**(`unpkg.com/lucide@latest`)—— 无本地构建,Tailwind 类在浏览器内 JIT 编译。自定义 CSS(Google Fonts 的 `ZCOOL KuaiLe` / `Kosugi Maru` 萌系字体、Q 弹浮动 / 云朵动画、`.font-kids` 工具类、`.btn-pop` 点击反馈)都写在文件顶部的内联 `<style>` 块里。

修改 `lesson.html` 时,必须保持幻灯片结构契约:新增的每一屏都必须是 `<section class="slide-page ...">`,且为 `.slide-container` 的直接子元素,否则 scroll-snap 吸附和翻页计数会失效。每屏的背景色通过 Tailwind 任意值类设置(如 `bg-[#E3F2FD]`)。
