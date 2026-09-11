# Recipe UI Card

Use this reference when generating a final recipe, ingredient plan, visual summary, share card, image prompt, or UI-like output for a fresh-food result.

## When To Include

When the skill generates a completed recipe or ingredient-plan result, include a UI-style recipe card specification unless the user asks for text only.

Do not generate the card when the result is blocked because nutrient analysis is required but unavailable. In blocked cases, first explain what cannot be confirmed and ask whether the user wants to downgrade to a 10% add-on or provide data for nutrient analysis.

## Card Goal

The card should feel like a clean UI result card that the user can screenshot, recreate in design software, or turn into a social-video overlay. The provided reference is for color, hierarchy, and information layout only; do not assume the final output must be a mobile vertical screen.

It must include:

- a pie chart or donut chart showing ingredient share;
- a clear ingredient list with food names and approximate cooked weights;
- a separate supplement list if supplements are included;
- a short data-source note;
- a short risk reminder or caveat.

## Visual Structure

Default layout: a flexible UI-style information card. Choose horizontal, square, or vertical proportions based on the user's use case. If no format is specified, provide a neutral card spec rather than forcing a specific aspect ratio.

Use this structure:

1. **Header**
   - title: `配方清单` or `本次搭配参考`;
   - subtitle: dog name, date, and path such as `10% 加餐` or `单次鲜食记录`.
2. **Ingredient Share Panel**
   - pale green or warm off-white background;
   - title: `食材占比`;
   - small note: `按食材熟重估算；补充项单独列出`;
   - donut chart on the left;
   - center label: total ingredient weight, such as `95.4 g 食材合计`;
   - legend on the right with color dot, ingredient name, approximate weight, and percentage.
3. **Ingredient List Panel**
   - title: `完整食材列表`;
   - count: such as `7 项食材`;
   - each row: ingredient name, preparation state, rough energy note if known, approximate weight.
4. **Supplement Panel**
   - title: `补充项`;
   - count: such as `2 项补充`;
   - list supplements separately from ingredients;
   - if none, write `本次未记录补充项`.
5. **Footer Notes**
   - data-source note in one short line;
   - risk reminder in one short line.

## Pie Or Donut Chart Rules

Use food weight percentages by default for the visual chart because this is easiest for users to understand in a recipe card.

Always label the chart as a visual composition, not as a scientific nutrition ratio:

```text
按食材熟重估算；补充项单独列出
```

If the user asks for a calorie chart, use calorie share instead and label it clearly:

```text
按估算热量占比；补充项单独列出
```

Do not call the chart an NRC ratio, AAFCO ratio, balanced ratio, or complete nutrition chart.

## Color Direction

Use a calm, natural palette:

- deep green for main protein;
- sage green for vegetables;
- warm ochre for larger vegetable or starch components;
- muted coral for small additions;
- soft blue-gray or olive for trace additions;
- off-white card background.

Keep text dark and readable. Avoid loud neon colors, medical-dashboard styling, or overly decorative elements.

## Output As Text Spec

If the assistant cannot directly create an image, output a structured card spec like this:

```text
UI 卡片
- 标题：
- 副标题：
- 卡片尺寸：按使用场景选择；未指定时不强制固定比例

食材占比图
- 图表类型：环形图
- 计算口径：按食材熟重估算，补充项单独列出
- 中心文字：
- 图例：
  - 食材 A：约 __ g，__%
  - 食材 B：约 __ g，__%

完整食材列表
- 食材 A（熟制方式）：约 __ g
- 食材 B（熟制方式）：约 __ g

补充项
- 补充项 A：约 __

页脚
- 数据来源提示：
- 风险提醒：
```

## Image Prompt Template

If an image-generation tool is available and the user asks for an actual image, use a prompt like:

```text
Create a clean UI-style recipe card for a cooked dog fresh-food meal. Use the reference only for color and hierarchy: off-white background, pale green ingredient-share panel, donut chart with total weight in the center, color-dot legend, full ingredient list in clean white panels, separate supplement section, small footer notes for data source and safety caveat. Calm natural palette: deep green, sage, ochre, muted coral, blue-gray, olive. Chinese UI text, large readable type, modern app-like information design, no medical claims, no brand logos. Do not force a specific aspect ratio unless the user asks for it.
```

Include the actual ingredient names, approximate amounts, and caveat text in the prompt when available. Keep the caveat short enough to remain readable.
