# Nutrient Analysis Gate

Use this reference when the user asks for:

- single-meal replacement;
- partial replacement above the 10% add-on path;
- an all-fresh-food meal;
- transition to fresh food;
- long-term homemade feeding;
- whether a food combination is nutritionally adequate.

## Core Rule

Do not generate a full meal replacement or repeatable homemade-feeding plan from calories alone.

Calories answer “how much energy”. They do not answer whether the food provides enough calcium, phosphorus, trace minerals, fatty acids, vitamins, amino acids, or safe upper-limit control.

## Path Decision

Classify the request before calculating:

1. **10% add-on**: can proceed with daily calorie budget, ingredient safety, and rough grams if data is sufficient.
2. **One-off single-meal replacement**: can estimate the meal's calories and give a cautious one-time structure, but must say it is not a repeatable balanced template unless nutrient analysis is available.
3. **Above 10%, transition, or long-term homemade feeding**: requires nutrient-level NRC analysis. If no reliable nutrient calculation engine is available, do not output a recipe amount table as if it solves the meal.

## Required for Nutrient-Level Analysis

To check whether a homemade meal or recipe is nutritionally adequate, require:

- confirmed dog profile and planned daily calories;
- each ingredient matched to a reliable food composition item;
- cooked/raw state and edible amount;
- nutrient data beyond calories, not just kcal;
- intended share of daily calories, such as 50%, 75%, or 100%;
- supplement details, including calcium source when relevant;
- comparison against NRC needs, recommended allowances, and safe upper limits.

If these are missing, say the analysis cannot be completed yet.

## When Only A Few Ingredients Are Provided

If the user provides a small ingredient set, such as lean beef + cucumber + tomato, and asks to replace a meal or feed all fresh food:

- do not expand the ingredients to meet calories as the main answer;
- do not say the meal is fine because the total kcal matches;
- do not call vegetable weight ratios “NRC” or “balanced”;
- state that the combination can be treated as a one-off fresh-food attempt only if the dog tolerates it, but it is not enough evidence for repeat feeding;
- name likely missing categories without pretending to calculate them precisely.

Suggested wording:

```text
这组食材可以估算热量，但不能只靠热量判断“这一顿是否营养达标”。如果它是 10% 加餐，可以继续按加餐额度处理；如果它要替代一整顿或经常这样吃，需要做 NRC 营养缺口审计。当前只给了几种食材，我不能把它包装成完整配方。
```

Likely gap categories to mention when appropriate:

- calcium and calcium/phosphorus balance;
- iodine, zinc, copper, manganese, selenium;
- vitamin D, vitamin E, some B vitamins;
- essential fatty acids;
- organ, calcium source, and broader ingredient variety.

## Output Template for Blocked Nutrient Analysis

Use this structure when nutrient analysis is required but unavailable:

```text
一句话判断
- 这次不能只按热量生成整顿替代方案；需要先做营养缺口审计。

路径判断
- 当前更像：整顿替代 / 高于 10% 鲜食 / 长期自制
- 这已经超出普通 10% 加餐逻辑。

可以先确认的部分
- 每日能量参考：
- 本餐目标热量：
- 食材安全和熟制提醒：

不能确认的部分
- 钙磷比例：
- 微量元素：
- 维生素：
- 必需脂肪酸：
- 是否适合长期重复：

数据来源提示
- 热量和营养需要分别来自不同数据：每日能量可按 NRC 思路估算；食材营养需要可靠食物成分数据和完整计算，不能由食材名直接推断。

风险提醒
- 这只是基于当前信息的自用判断，不能替代兽医或兽医营养师建议；整顿替代、长期自制或有健康问题时，请先做专业确认。

下一步
- 你要把它降级成一次 10% 加餐，还是补充完整食材和补剂信息后做营养缺口审计？
```

## If Nutrient Analysis Is Available

If a reliable local calculator or user-provided nutrient table is available, the answer may run nutrient-level analysis. In that case:

- compare per-day or per-1000-kcal nutrient values against NRC needs, recommended allowances, and safe upper limits;
- show missing, low, adequate, and excessive categories;
- keep AAFCO separate unless authorized and verified data is actually available;
- still include data source and risk reminders.
