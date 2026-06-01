# Keyword Routing

Use this table to lock the task type before reading `pdf-prompt-index.md`.

## Platform Keywords

- `meituan-menu`: 美团, 外卖, 菜单主图, 平台主图, 外卖平台
- `dianping-menu`: 大众点评, 点评, 菜单图, 美团菜单, 大众点评菜单
- `douyin-cover`: 抖音, 本地生活, 短视频封面, 竖屏封面, 团购封面, 探店封面, 点击率
- `moments-poster`: 朋友圈, 微信朋友圈, 社群, 老板发圈, 日常宣传, 到店宣传
- `general-poster`: 小红书, 种草, 笔记封面, 探店笔记, 店内海报, 门店海报, 桌贴, 易拉宝, 横版海报

## Scene Keywords

- `single-dish`: 单品, 单道菜, 招牌菜, 主推菜, 菜品图, 一道菜, 菜名
- `combo`: 套餐, 双人餐, 家庭餐, 工作餐, 团购套餐, 菜品列表, 多人餐
- `promotion`: 促销, 优惠, 活动, 限时, 特价, 秒杀, 低价, 买一送一, 立减
- `new-product`: 新品, 上新, 新品上市, 限时尝鲜, 今日推荐
- `menu-price-list`: 菜单, 价目表, 价格表, 产品列表, 菜单排版
- `qr-lead`: 扫码, 二维码, 进群, 领券, 微信, 咨询, 扫码下单
- `opening`: 开业, 新店, 试营业, 新店开业, 开业福利
- `holiday`: 节日, 端午, 中秋, 国庆, 春节, 520, 七夕, 元旦
- `quality-explain`: 品质说明, 食材新鲜, 分量足, 现做现卖, 包装升级, 差评挽回
- `store-environment`: 门店环境, 店铺环境, 包间, 装修, 干净舒适, 聚餐环境

## Dish-Type Keywords

- `hotpot`: 火锅, 串串, 涮菜, 肥牛, 毛肚, 鸭血, 火锅菜品
- `barbecue-night`: 烧烤, 烤鱼, 小龙虾, 串, 夜宵, 宵夜, 烤串
- `breakfast`: 早餐, 包子, 豆浆, 油条, 面, 粉, 粥, 热乎
- `light-meal`: 轻食, 减脂餐, 沙拉, 健身餐, 鸡胸肉, 低卡
- `drink`: 奶茶, 咖啡, 果茶, 饮品, 杯身, 清爽
- `dessert-snack`: 甜品, 蛋糕, 小吃, 炸香蕉, 酥脆, 特色小吃
- `student-worker-meal`: 学生党, 打工人, 管饱, 实惠, 出餐快, 写字楼, 学校周边

## Style And Purpose Keywords

- `clean-premium`: 高级, 干净, 简洁, 品牌感, 留白, 不廉价
- `street-real`: 烟火气, 夜市, 街边, 热闹, 真实店铺
- `fresh-light`: 清爽, 新鲜, 浅绿, 白色背景, 低油, 健康
- `warm-appetite`: 暖光, 食欲, 热乎, 火锅氛围, 聚餐
- `click-through`: 点击率, 吸引点击, 强吸引, 封面, 一眼想点
- `conversion`: 下单, 到店, 引流, 团购, 扫码, 进群, 提升转化

## Conflict Rules

- If a platform keyword exists, it controls aspect ratio and layout density.
- If both `douyin-cover` and a dish type exist, keep Douyin as primary. Do not merge dish-type template wording into the final prompt.
- If both `meituan-menu` and `promotion` exist, choose one primary template. Do not combine two template bodies.
- If `qr-lead` appears, reserve a clean QR position even when another scene is primary.
- If `menu-price-list` appears with many dishes, prioritize readable menu layout over food-photo drama.
- If only `clean-premium` is clear, route to `premium-poster`.
- Style and purpose keywords are supporting signals only. Except `clean-premium` -> `premium-poster`, do not treat them as standalone templates.
- If no keyword is clear, route to `general-poster`.
