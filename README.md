# WGHGs Paper Tracker

这是一个面向“内陆水体温室气体”的静态文献追踪网页。检索主题聚焦河流、湖泊、水库、池塘、溪流、沟渠、潮沟、湿地等水体中的 CO2、CH4、N2O 和 greenhouse gas 研究。

## 研究方向

- 水体对象：inland water、freshwater、river、stream、creek、lake、reservoir、pond、ditch、canal、channel、tidal creek、tidal channel、wetland、marsh、estuary 等
- 温室气体：CO2 / carbon dioxide、CH4 / methane、N2O / nitrous oxide、greenhouse gas / greenhouse gases
- 分类标签：process、flux、isotope、nutrient、microbial、urban、agriculture

注意：分类标签不作为默认检索词。默认检索只使用“水体对象 + 温室气体”组合，分类标签仅根据题名、摘要和期刊信息自动打标。

## 免费发布到 GitHub Pages

1. 在 GitHub 新建仓库 `WGHGs`。
2. 把本文件夹内容推送到仓库 `main` 分支。
3. 打开仓库 `Settings` → `Pages`。
4. 在 `Build and deployment` 中选择 `Deploy from a branch`。
5. Branch 选择 `gh-pages`，Folder 选择 `/ (root)`。
6. 打开 `Actions` 页面，手动运行一次 `Update papers and deploy`。

发布后，网页地址通常是：

```text
https://你的用户名.github.io/WGHGs/
```

## 自动更新

`.github/workflows/update-and-deploy.yml` 默认每天 UTC 21:18 运行一次，对应中国时间次日 05:18。它会：

1. 从 Semantic Scholar 发现论文。
2. 用 Semantic Scholar 统一回填引用数、参考文献数、开放 PDF、代表性参考文献和相似文章。
3. 合并到 `data/papers.json`。
4. 发布静态网页到 `gh-pages` 分支。

建议添加 GitHub Actions 变量：

```text
CONTACT_EMAIL=你的邮箱
```

建议添加 GitHub Actions Secret：

```text
SEMANTIC_SCHOLAR_API_KEY=你的 Semantic Scholar API key
```

## 本地预览

```bash
python -m http.server 8010
```

然后打开：

```text
http://localhost:8010
```

## 调整检索式

如果想扩大或收窄文献范围，编辑 `scripts/update_papers.py` 里的：

- `ENVIRONMENT_TERMS`
- `GHG_TERMS`
- `ENVIRONMENT_GROUPS`
- `GHG_GROUPS`

分类标签由 `TAG_RULES` 控制。

## 数据来源与致谢

本项目使用开放学术数据服务构建文献追踪页面。感谢这些服务提供 API、元数据和开放学术基础设施：

- Semantic Scholar：统一回填引用数、参考文献数、代表性参考文献、开放 PDF、摘要、相似文章和学术图谱信息。
- OpenAlex、Crossref、PubMed：当前不作为默认数据源；如以后需要扩大覆盖，可手动启用。

网页不会在浏览器端直接调用 Semantic Scholar API，因此不会暴露 API key。相似文章、引用指标和参考文献信息由 GitHub Actions 在后台预计算后写入 `data/papers.json`。
