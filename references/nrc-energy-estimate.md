# NRC-Style Daily Energy Estimate

Use this reference when the user asks to calculate daily intake, planned calories, MER, 10% fresh-food add-on budget, or meal allocation.

## Scope

This workflow estimates daily energy intake for a healthy adult dog in maintenance. It does not calculate a complete nutrient profile and must not be presented as a full NRC-compliant recipe.

Every output that includes an energy estimate, calorie budget, ratio, or concrete feeding suggestion must include both:

- a brief data source note;
- a brief risk reminder.

Allowed wording:

- 基于 NRC 思路估算每日能量需求。
- 每日能量摄入参考 / 计划热量。
- 这个结果用于确定“每天大概吃多少热量”和“鲜食加餐占多少热量”。

Avoid wording:

- NRC 标准配方。
- 这顿饭符合 NRC。
- 这份搭配完整均衡。
- 按 NRC 推荐的肉菜比例。

## Required Inputs

Before estimating, confirm:

1. current body weight in kg;
2. life stage is adult maintenance;
3. approximate body condition: thin, normal, slightly overweight, overweight, or BCS score;
4. activity level: low, typical, high, or unknown;
5. neuter status if available;
6. current stable daily intake if the user knows it.

If weight is missing, do not calculate. Ask for weight first.

If activity level is unknown, present a range rather than silently choosing one value.

## Veterinary Gate

Do not provide a precise planned-calorie target for:

- puppies;
- pregnancy or lactation;
- kidney, liver, heart disease;
- pancreatitis history;
- active obesity treatment or prescribed weight loss;
- chronic gastrointestinal symptoms;
- prescription diets;
- elimination diets or complex allergies;
- unexplained vomiting, diarrhea, appetite change, or rapid weight change.

In these cases, you may still organize the profile and explain what information a veterinarian or veterinary nutritionist would need.

## Estimate Logic

Use metabolic body weight as the base:

```text
metabolic body weight = body weight kg ^ 0.75
```

For healthy adult maintenance, estimate MER as:

```text
MER = k × body weight kg ^ 0.75
```

Use conservative k values:

- low activity or neutered adult: about 95 kcal × kg^0.75;
- typical adult maintenance: about 110 kcal × kg^0.75;
- active adult: about 130 kcal × kg^0.75.

If the user provides a known stable daily intake and the dog's weight and body condition are stable, treat it as important calibration context. Do not override real stable intake with a formula without explaining the difference.

## Presenting the Result

Give the result as a range or a reference value, then ask for confirmation.

Example:

```text
按目前信息，它更接近健康成年犬维持期。我可以先用 NRC 思路估一个每日能量参考：

- 低活动：约 ___ kcal/天
- 日常活动：约 ___ kcal/天
- 较高活动：约 ___ kcal/天

这不是完整营养配方，只是用来确认“每天总热量”和后面鲜食加餐额度的参考。你觉得它平时更接近哪一种活动量？
```

## Data Source Note

When using numbers, briefly explain their source type:

- NRC-style energy logic for daily maintenance calorie estimates;
- public food composition data for generic ingredient calories or nutrients;
- package label data for commercial food, supplements, or branded products;
- user-provided values when the exact ingredient, brand, cooked weight, or label is not in the available data.

Recommended wording:

```text
数据来源提示：每日能量按 NRC 思路估算；食材热量会参考公开食物成分数据、包装标签或你提供的信息，因此只能作为近似参考。
```

Do not cite an exact database, publication, brand label, or product version unless that source is actually available for the current result.

## Risk Reminder

For any calculation or plan, include a compact reminder:

```text
风险提醒：这只是基于当前信息的自用参考，不能替代兽医或兽医营养师建议；如果狗狗有疾病、处方粮、过敏、肠胃异常或体重管理需求，请先咨询专业人士。
```

## 10% Add-On Budget

If the user chooses the 10% fresh-food add-on path, calculate the optional add-on budget from planned daily calories:

```text
fresh-food add-on budget = planned daily kcal × 10%
```

State clearly:

- 10% means calories, not food weight.
- Fresh food, treats, table food, and unverified homemade add-ons share this budget.
- The user does not need to use the full 10% every day.
- A 10% add-on is different from long-term homemade main feeding.

## Meal Allocation

Daily calories are the baseline. Meals only split the daily plan; they do not create new daily targets.

If the user eats 2 meals per day and chooses equal allocation:

```text
each meal = planned daily kcal × 50%
```

For a single meal fresh-food add-on, still calculate the add-on from the daily budget unless the user clearly wants a different meal plan.
