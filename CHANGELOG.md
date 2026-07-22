# Changelog

本项目的所有重要变更记录。格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

## [2.1.0] - 2026-07-22

### 变更

- 项目更名:landing-craft → **Landfall** 🏝️,skill 内部名 citycraft → landfall,纳入舰队命名体系
- 仓库以全新 history 重建于 [can4hou6joeng4/Landfall](https://github.com/can4hou6joeng4/Landfall),旧版本 release 记录见本文件
- 上游致谢链接(oil-oil/citycraft)保留不变

## [2.0.0] - 2026-04-15

### 新增

- 日文版项目说明文档（README.ja.md）
- 评估用例扩展至 9 条，新增多页面站点、日文触发、极简输入容错三类边界场景
- 中英日三语 README 导航互链

### 优化

- CI 断言更新为 9 条 evals 基线

## [1.9.0] - 2026-04-15

### 优化

- 重新设计中英文 README，结构更简洁清晰
- 新增 "Why Landing Craft?" 差异化价值说明
- 功能列表从扁平罗列重组为三个分组（设计系统/页面板块/工作流）
- 添加 Stars 徽章和居中标题布局
- 项目结构收入折叠面板减少首屏长度
- 全部 section 标题添加语义化 emoji 增强扫读体验
- 中英文 README 结构完全对齐

## [1.8.0] - 2026-04-14

### 新增

- 中文版项目说明文档
- 演示站点增强（GSAP 动画 + clip-path 分隔线 + 城市风格滚动预览 + 计数动画）
- 英文 README 和中文 README 互链

## [1.7.0] - 2026-04-14

### 新增

- 在线演示站点部署到 GitHub Pages
- README 新增 Release 和 License 徽章和快速导航链接

## [1.6.0] - 2026-04-14

### 新增

- 6 种扩展板块变体（团队成员/数据统计/品牌滚动墙/作品集/技术集成/时间线）
- GitHub Actions CI 自动化测试（Python 3.9 + 3.12 双版本验证）
- CI 徽章添加到 README

### 修复

- 推荐页面序列补充 Footer 和 Form 板块
- 新增 Startup pre-launch 推荐序列

## [1.5.0] - 2026-04-14

### 新增

- 暗色模式运行时切换功能（localStorage 持久化 + 系统偏好检测）
- 部署支持扩展至 Netlify、Vercel、GitHub Pages 三个平台

### 修复

- 修复 Footer、Form、Page 变体未接入工作流的问题
- Step 1 新增子页面需求询问环节
- Step 3 补充 footer/form/pages 字段选择说明

## [1.4.0] - 2026-04-14

### 新增

- 3 种表单板块变体（邮件订阅/等待列表/内嵌联系表单）
- 全部表单组件符合无障碍标准和触控目标规范

## [1.3.0] - 2026-04-14

### 新增

- 一键部署到 Netlify 的可选步骤（先预览后发布两步式部署）

## [1.2.0] - 2026-04-14

### 新增

- 多页面站点生成支持（关于我们/联系方式/博客列表三种子页面模板）
- 子页面共享同一设计系统、导航和页脚
- SKILL.md 工作流和资产表同步更新

## [1.1.0] - 2026-04-14

### 新增

- 全部 8 个 GSAP 动画函数支持 prefers-reduced-motion 无障碍降级
- Design Laws 新增响应式布局、SEO 基线、Footer 必须、无障碍基线四条规则
- 3 种 Footer 板块变体（极简单行/多列链接/杂志编辑型）
- Step 5 生成完成后自动在浏览器中打开预览
- 预览页面语言根据用户对话语言自动检测

## [1.0.0] - 2026-04-13

### 新增

- 57 种城市风格设计系统
- 浏览器交互式风格预览（style-preview）和选项选择（options-preview）
- 7 种 Hero 板块变体（A-G）
- 6 种 Features 板块变体（A-F）
- 6 种 Testimonials 板块变体（A-F）
- 6 种 Conversion 板块（定价/对比定价/品牌墙/CTA/FAQ×2）
- 4 种导航风格（全屏爆开/磁性胶囊/侧边垂直/拆分居中）
- 3 种色调变体（原色/暗黑/提亮）
- GSAP ScrollTrigger 动画库（8 个预制函数）
- CSS 纹理库（6 种）和 clip-path 分隔线库（8 种）
- 跨平台预览启动器（Python + PowerShell）
- 端口占用自动 fallback 机制
- 日文城市名查询支持（CJK 别名映射）
- 非城市描述的设计推导路径（imagery-derivation）
- 6 个评估用例覆盖所有主要路径
