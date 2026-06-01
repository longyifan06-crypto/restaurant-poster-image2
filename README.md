# restaurant-poster-image2

一个用于餐饮商家宣传图生成的 Codex skill。

一句话介绍：这是一个“餐饮宣传图 AI 接单助手”，专门把商家随手拍的菜品原图，结合店名、菜名、价格、活动、平台关键词，自动匹配餐饮海报提示词，并用 image2.0 生成更适合发布的商业宣传图。

它适合地推餐饮商家时使用：你提供菜品原图、店名、菜名、价格、平台、场景关键词等信息，skill 会先根据关键词锁定任务类型，再匹配内置的餐饮宣传图提示词索引，最后调用 image2.0 / image generation 生成可直接发美团、大众点评、朋友圈、抖音本地生活或小红书的宣传图。

适合人群：想用 AI 给小餐饮店做宣传图、美团菜单图、抖音团购封面、朋友圈海报，并把它变成低成本接单服务的人。

## 能做什么

- 菜品单图宣传图
- 美团 / 大众点评 / 外卖菜单图
- 抖音本地生活封面
- 朋友圈日常宣传图
- 新品上市、开业活动、节日营销
- 套餐 / 团购 / 学生党 / 打工人套餐图
- 二维码引流海报
- 门店环境宣传图
- 价目表 / 菜单价格图

## 工作方式

1. 读取用户给的菜品图和文字信息。
2. 根据关键词判断任务类型，例如“美团、菜单图、抖音封面、新品、扫码、火锅、夜宵、朋友圈”。
3. 从 `references/pdf-prompt-index.md` 中匹配合适的餐饮提示词模板。
4. 组装 image2.0 可执行的出图提示词。
5. 直接生成图片，并简短说明匹配到的任务类型和模板。

## 安装

克隆仓库后，把 skill 目录复制到本地 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R skills/restaurant-poster-image2 ~/.codex/skills/
```

然后在 Codex 中这样调用：

```text
用 $restaurant-poster-image2，把这张菜品图做成美团菜单图。
菜名：牛肉面
价格：18
关键词：外卖主图、干净、高级、食欲感
```

## 示例

```text
用 $restaurant-poster-image2 做一张抖音本地生活封面。
菜品：夜宵烧烤
价格：9.9 起
关键词：抖音封面、夜宵、烧烤、朋友聚餐、暖光
```

```text
用 $restaurant-poster-image2 做一张扫码进群海报。
菜品：火锅双人套餐
活动：进群领券
关键词：扫码、二维码、火锅、套餐、引流
```

## 目录结构

```text
skills/restaurant-poster-image2/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── keyword-routing.md
    └── pdf-prompt-index.md
```

## 说明

这个仓库不包含原始 PDF 文件，只包含从餐饮宣传图工作流中提炼出的提示词索引和关键词路由规则。

## License

MIT
