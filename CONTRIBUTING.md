# 贡献指南

感谢你对 Landfall 的关注！欢迎任何形式的贡献。

## 如何贡献

### 报告问题

使用 [Issue 模板](https://github.com/can4hou6joeng4/Landfall/issues/new/choose) 提交 Bug 报告或功能建议。

### 提交代码

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feat/你的功能`
3. 提交改动，commit message 格式：`type: 中文描述`
   - `feat:` 新功能
   - `fix:` Bug 修复
   - `docs:` 文档更新
   - `refactor:` 重构
   - `chore:` 工程配置
4. 推送并创建 Pull Request

### Commit Message 规范

```
type: 简洁的中文描述
```

示例：
- `feat: 新增城市风格哥本哈根`
- `fix: 修复预览端口冲突`
- `docs: 更新安装说明`

### 添加新城市风格

1. 在 `references/city-styles.md` 中添加城市条目，包含所有 6 个必须子章节：Fonts、Colors、Texture、Layout character、Motion character、Icons
2. 在两个模板 HTML 中添加对应的预览卡片
3. 如有日文名，在 `assets/scripts/get_city_tokens.py` 的 `CJK_ALIASES` 中添加映射
4. 运行验证：`python3 assets/scripts/get_city_tokens.py "城市名"`

### 添加板块变体

1. 在对应的 `assets/sections/*.html` 中用 `<!-- @@VARIANT:X -->` 标记包裹
2. 更新 `SKILL.md` 中 Step 4b 的变体表格
3. 运行验证：`python3 assets/scripts/extract_variant.py <file> <variant>`

## 开发环境

- Python 3.6+
- 任意现代浏览器（预览功能）
- Claude Code（测试 skill 工作流）
