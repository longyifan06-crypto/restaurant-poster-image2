---
name: restaurant-poster-image2
description: Use this skill when the user wants to generate restaurant, food, dish, menu, Meituan, Dianping, delivery, Douyin local-life, Xiaohongshu, Moments, QR-code, opening, promotion, combo, or catering poster images from dish photos and merchant information with image2.0 or image generation. The skill routes user-provided keywords to the closest original PDF-derived Chinese prompt template, asks once for optional missing details, replaces only template placeholders, never privately rewrites the prompt, then generates the image.
---

# Restaurant Poster Image2.0

Generate restaurant promotional images from dish photos and merchant details. This skill selects an original Chinese prompt template from a PDF-derived restaurant poster workflow and sends that template to image2.0 without private rewriting.

## Default Behavior

- Use the user's dish image as the visual truth, but do not add private prompt clauses beyond the selected original template.
- First route the request by keywords, then read `references/pdf-prompt-index.md` for the matching original Chinese prompt template.
- After receiving the dish photo and initial merchant information, ask the user once whether they want to supplement several useful details. Do not generate before this one supplement check unless the user explicitly says to skip questions or generate directly.
- If the user says no, "不用", "没有", "按现有信息", or "直接做", proceed with the existing information and do not ask again.
- If the scene cannot be confidently matched from the user's keywords, always use `general-poster` ("通用海报提示词").
- Do not add aspect ratio, style, layout, or quality words unless they are already in the selected PDF template or explicitly provided by the user.
- Chinese text is generated directly in the image by image2.0 unless the user asks for a more reliable local text overlay workflow.

## Inputs To Extract

Extract these fields from the user message and attached images:

- dish image role: main dish photo, menu photo, storefront photo, QR code, logo, or style reference
- keywords: platform, scene, dish type, purpose, style
- store or brand name
- dish or combo name
- price, discount, activity, date, business hours
- selling points: fresh, large portion, signature, low price, new product, group meal, made now, suitable for hotpot, clean environment
- required text: phone, address, WeChat, QR code, slogan
- fixed constraints: do not alter dish shape, plate, package, logo, QR position, store environment
- output count and whether multiple images need a consistent style

Do not invent missing store names, prices, phone numbers, addresses, QR codes, logos, or dates. If a missing field is important, omit that text or use a generic short selling point.

## One-Time Supplement Check

After the user sends a dish photo plus any initial information, reply with a short supplement checklist before generating. The checklist should collect fields needed to choose a PDF scene template or replace `【】` placeholders. Do not use the checklist as permission to invent or rewrite the final prompt.

Use this structure:

```text
我先按现有信息判断是：<matched task type>。
出图前你还要补充这几点吗？没有的话，我就按现在的信息直接生成：
1. <missing or useful point>
2. <missing or useful point>
3. <missing or useful point>
```

List 3-6 points at most. Prefer these points:

- 用在哪个平台或比例：美团/大众点评/外卖、抖音封面、小红书、朋友圈、店内海报。
- 必须写在图上的文字：店名、菜名、价格、活动、营业时间、电话、地址。
- 想突出的卖点：新鲜、分量足、便宜、招牌、现做、适合聚餐、出餐快。
- 想要的风格：高级干净、烟火气、年轻潮流、火锅氛围、轻食清爽。
- 不能改的地方：菜品形状、盘子、包装、LOGO、二维码位置、门店环境。
- 是否需要多张图以及是否统一风格。

If the routed task has special needs, include them in the checklist:

- Meituan/menu: ask whether price and one-line selling point should appear.
- Douyin cover: ask for a short headline under 8 Chinese characters if not provided.
- QR lead: ask for QR code placement and whether a QR image will be supplied.
- Combo/menu price list: ask for dish list and prices if incomplete.
- Store environment: ask what area to emphasize, such as private room, storefront, or dining area.

Once the user answers, use their additions only for scene routing and placeholder replacement. If they confirm no additions, generate immediately with the closest original template or `general-poster`.

## Keyword Routing

Read `references/keyword-routing.md` when the user gives keywords, platform names, scene words, or ambiguous intent.

Routing priority:

1. Platform: Meituan/Dianping/delivery, Douyin, Xiaohongshu, Moments, in-store poster.
2. Scene: single dish, combo, promotion, new product, opening, holiday, price list, QR lead generation, storefront/environment, quality explanation.
3. Dish type: hotpot, barbecue, night snack, breakfast, light meal, drink, dessert, snack.
4. Purpose: attract clicks, menu upgrade, group-buying cover, get customers to store, scan code, show value, recover trust.
5. Style: clean premium, lively street-food, young trendy, warm hotpot, fresh light-meal.

When multiple signals appear, choose one primary template by `platform > scene > dish type > purpose > style`. Do not merge extra prompt language from secondary templates. Example: "Douyin cover + night snack + barbecue" uses the Douyin-cover template as the final prompt template; do not paste barbecue-night text into it unless the user explicitly asks.

If the user only provides a dish image and dish name but no scene keyword, use `general-poster`. Use `single-dish` only when the user clearly indicates 单品、菜品图、招牌菜、主推菜, or a similar single-dish scene. If the scene is unclear or required placeholders cannot be safely filled, use `general-poster`.

## Prompt Fidelity Rules

The final image2.0 prompt must be the selected template text from `pdf-prompt-index.md`, with only these allowed changes:

- Replace bracket placeholders such as `【店名】`, `【菜品名】`, `【价格】`, `【活动主题】` with the user's exact supplied text.
- If the user explicitly adds a required detail, place it only where the template already has the corresponding placeholder or instruction.
- If no matching template is clear, use `general-poster` exactly.

Never do these:

- Do not translate the Chinese template into English.
- Do not paraphrase, beautify, shorten, expand, or reorder the template.
- Do not combine two PDF templates into one new prompt.
- Do not add new photography/style/layout words from your own judgment.
- Do not invent missing store names, prices, phone numbers, addresses, QR codes, logos, or dates.
- Do not add a separate "negative prompt" unless the selected original template already contains those negatives.

## Generation

- Use built-in image generation/image2.0 by default.
- If the user supplied a local image file path, inspect it first so the image is visible in the conversation before using it as the dish reference.
- For one final image, make one image generation call.
- For multiple requested images or variants, make one generation call per distinct deliverable so each prompt can match its scene.
- After generation, briefly report:
  - matched task type
  - matched PDF-derived template
  - aspect ratio
  - any omitted missing fields
  - final image result

## Quality Check

Before finalizing, check:

- Dish still looks like the original photo.
- Food looks clean, real, appetizing, and not over-filtered.
- Layout is not cluttered and avoids cheap red-yellow ad clutter unless explicitly requested.
- Text is short: title 8-12 Chinese characters when possible, one subtitle, price visible if provided.
- Platform ratio matches the routed task.
- Required fixed elements are preserved or correctly reserved.
- No invented price, phone, address, QR code, logo, or impossible claim.
- No obvious garbled text. If text accuracy is weak, tell the user and suggest a "stable text overlay" version.
