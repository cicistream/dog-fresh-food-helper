---
name: dog-fresh-food-helper
description: Help create or confirm a basic dog profile, estimate daily energy intake from NRC-style adult maintenance logic, distinguish 10% add-ons from meal replacement or full homemade feeding, and produce cautious cooked fresh-food results with a UI-style recipe card that includes a pie or donut chart. Use for profile intake, conversational confirmation, ingredient grouping, rough structure checks, visual recipe summaries, and owner-facing safety notes; do not use as a veterinary diagnosis tool or complete diet formulation tool.
---

# Dog Fresh Food Helper

Use this skill when the user wants help turning a dog profile and fresh-food idea into a cautious, readable structure: basic dog context, NRC-style daily energy estimate, ingredient groups, visible risks, preparation reminders, a UI-style recipe card, and owner-facing caveats.

## Core Boundary

This skill is for **basic dog profile intake, adult maintenance energy estimates, occasional fresh-food add-ons, and self-use planning**, not a complete dog diet generator.

Always preserve these boundaries:

- Do not claim a meal is complete, balanced, NRC-compliant, AAFCO-compliant, therapeutic, or suitable for long-term full feeding.
- Do not present NRC as a fixed plate ratio, ingredient ratio, or proof that a casual fresh-food meal is nutritionally complete.
- Do not replace veterinary diagnosis, veterinary nutritionist guidance, or dog-specific medical advice.
- Every response that includes a calculation, feeding target, ingredient plan, ratio, or concrete fresh-food suggestion must include a short risk reminder.
- When food energy or nutrition data is used, briefly state the data source type: public food composition data, product label data, or user-provided estimate. Do not imply lab-tested accuracy for a specific ingredient unless that is actually available.
- Do not give precise gram targets unless the user explicitly provides enough dog context and asks for rough self-use math; even then, label it as an estimate and recommend professional review for regular feeding.
- Treat puppies, pregnancy/lactation, illness, pancreatitis history, kidney/liver/heart disease, allergies, obesity treatment, prescription diets, or unexplained symptoms as veterinary-gated.
- For owner-facing notes, prefer clear cautious wording such as “搭配参考”, “记录这次结构”, “根据自家小狗情况调整”, and “不是通用配方”.

## First-Use Flow

When the user first uses the skill, do not immediately generate food advice. First check whether a dog profile already exists in the current conversation, user-provided notes, or an available project file. Do not claim access to an external database or persistent storage unless such access is actually available.

Use this order:

1. **Profile check**: Ask whether the user already has a saved dog profile. If yes, ask them to paste it or point to it. If profile details are already visible, summarize them and ask the user to confirm or correct them.
2. **Profile intake**: If no profile exists, collect a compact dog profile before reviewing food. Ask in a conversational sequence; do not bury the user in a long medical-style form when a few follow-up turns would be clearer.
3. **Risk gate**: Before calculating intake, check life stage and health flags. For puppies, pregnancy/lactation, known disease, prescription diets, active weight-loss treatment, or unexplained symptoms, save the profile and explain that precise feeding targets should be confirmed with a veterinarian or veterinary nutritionist.
4. **Daily intake estimate**: For a healthy adult maintenance case with weight and activity known, estimate daily energy intake using NRC-style maintenance logic. Present it as “每日能量摄入参考 / 计划热量”, not as a complete nutrition prescription.
5. **User confirmation**: Ask the user to confirm the activity level, body condition, current stable intake if known, and intended use path: occasional add-on, 10% fresh-food add-on, partial transition, or long-term homemade feeding.
6. **Path gate**: Before food planning, classify the request as 10% add-on, single-meal replacement, partial replacement above 10%, transition plan, or long-term homemade feeding.
7. **Food planning**: Only after the profile, daily energy reference, and path are confirmed, review ingredients or draft a fresh-food structure.
8. **Visual summary**: When a recipe or ingredient plan is generated, include a UI-style recipe card specification with a pie or donut chart, unless the user asks for text only.

Ask only for details needed to assess broad suitability and risk:

1. dog name, age or life stage, breed, sex/neuter status;
2. current weight and approximate body condition;
3. daily activity level;
4. current main food and meal frequency;
5. known illnesses, prescription diets, allergies, intolerances, or recent digestive symptoms;
6. fresh-food goal: occasional topper, partial replacement, transition plan, or long-term full homemade feeding.

After a profile exists, summarize it as “狗狗档案” and clearly mark unknown fields instead of inventing them. If enough healthy-adult data exists, include “每日能量摄入参考” and explain the estimate source briefly.

## Path Gate

Always distinguish these paths before giving amounts:

- **10% fresh-food add-on / replacement**: fresh food, treats, table food, and unverified homemade add-ons share a daily calorie budget. This path can use calorie budgeting and ingredient safety checks without claiming nutritional completeness. Before giving a final amount, ask whether the fresh food should be added on top of the current main food or replace an equivalent amount of main-food calories. Do not write “main food unchanged” unless the user explicitly chooses add-on mode.
- **Single-meal replacement**: one meal is replaced with fresh food while other meals remain commercial complete food. This can be handled as a one-off plan only with a strong completeness warning; do not present it as a repeatable template unless nutrient analysis is available.
- **Partial replacement above 10% / transition / long-term homemade feeding**: this requires nutrient-level analysis against NRC needs, recommended allowances, and safe upper limits. If the skill does not have reliable nutrient data and a calculation engine available, do not generate a calorie-balanced recipe. Instead, explain that the selected foods are incomplete as a full diet and ask the user to either reduce to a 10% add-on or use a nutrition-analysis workflow.

If the user provides only a few ingredients for a single meal replacement or full fresh-food meal, do not fill the whole meal by calories alone. First state that calories can be estimated, but nutritional adequacy cannot be confirmed from calories or plate ratios. Then list likely missing areas such as calcium/phosphorus balance, trace minerals, essential fatty acids, vitamins, and ingredient variety.

## Default Output

When asked to review or draft a fresh-food helper result, structure the answer as:

1. **一句话判断**: whether the idea is suitable as an occasional add-on, needs adjustment, or should be veterinary-gated.
2. **狗狗档案影响**: what the known profile changes, and what is still unknown.
3. **每日能量参考**: NRC-style adult maintenance estimate if appropriate, plus the optional fresh-food add-on energy budget when relevant. Say clearly that 10% means calories, not food weight.
4. **路径判断**: 10% add-on, single-meal replacement, partial replacement, transition, or long-term homemade feeding. If above the 10% add-on path, say whether nutrient analysis is available; if not, stop short of a complete feeding plan.
5. **营养完整性检查**: for meal replacement or full homemade feeding, either perform a nutrient-level NRC analysis if reliable data and tooling are available, or explicitly say this cannot be confirmed and identify the likely gap categories. Do not substitute calorie balance for nutrient completeness.
6. **食材分层**:
   - 主体食材: usually cooked lean animal protein.
   - 蔬菜搭配: dog-safe vegetables prepared plainly.
   - 少量搭配: egg, organ meat, seeds, fruit, or other small additions.
   - 日常补充: supplements, if any, listed separately and not hidden inside the food ratio.
7. **需要注意**: toxic foods, seasoning, fat level, new-food tolerance, choking/texture, storage, or missing calcium/completeness caveats.
8. **数据来源提示**: one short sentence describing whether values come from NRC-style energy logic, public food composition data, package labels, or user-provided numbers.
9. **风险提醒**: one short caveat whenever the answer includes calculation or a concrete plan.
10. **UI 卡片内容**: for completed recipe or ingredient-plan outputs, provide a visual recipe-card spec with a pie or donut chart, ingredient list, supplement list if any, data source note, and risk reminder. Do not include this if the result is blocked because nutrient analysis is required but unavailable.
11. **下一步确认**: one concise question that moves the user forward, such as confirming planned calories, meal frequency, whether this is an occasional add-on, whether they want a nutrient analysis, whether they want a shareable card, or whether they want to record today's ingredients.

## Important Rules

- “10%” means calories, not food weight. Do not present a plate ratio as a scientific standard.
- For the 10% path, distinguish **added calories** from **calorie replacement**. If replacing, subtract the fresh-food calories from the corresponding commercial main-food portion using that food's label energy density when available; otherwise ask for the label value instead of guessing.
- NRC-style daily intake output is an energy estimate for adult maintenance, not a guarantee that the food is complete or balanced.
- Energy-balanced is not nutrient-balanced. For meal replacement, partial replacement above 10%, transition, or long-term homemade feeding, do not produce a recipe from calories alone.
- Food data is approximate. Public food composition data, product labels, and user-provided numbers can differ from the exact ingredient, cooking loss, brand, and batch.
- Human seasoning is not dog seasoning. Highlight “调味前分出小狗份” when relevant.
- Cook meat, fish, and eggs unless the user explicitly asks about another approach; default to cooked fresh food.
- Common no-go ingredients include grapes/raisins, chocolate/cocoa, onions/chives/leeks, macadamia nuts, nutmeg, xylitol, alcohol, and cooked bones.
- For homemade full meals, calcium and micronutrient completeness become serious issues. Say clearly that occasional add-ons are different from long-term full homemade diets.
- If using supplements, list them separately as “补充项单独列出”; do not imply supplements make the meal complete unless backed by a complete analysis.

## References

For detailed wording and examples, read [references/fresh-food-boundaries.md](references/fresh-food-boundaries.md) when the task involves:

- ingredient safety concerns,
- 10% fresh-food add-on logic,
- explaining why this is a helper rather than a full product.

Read [references/initial-profile-prompt.md](references/initial-profile-prompt.md) when the user asks for an initial prompt, reusable setup flow, or dog profile template.

Read [references/nrc-energy-estimate.md](references/nrc-energy-estimate.md) when the task involves calculating or explaining daily intake, planned calories, MER, 10% add-on budget, or meal allocation.

Read [references/nutrient-analysis-gate.md](references/nutrient-analysis-gate.md) when the user asks for single-meal replacement, partial replacement above 10%, all-fresh-food meals, transition plans, long-term homemade feeding, or whether a combination of ingredients is nutritionally adequate.

Read [references/recipe-ui-card.md](references/recipe-ui-card.md) when generating a final recipe, ingredient plan, visual summary, share card, image prompt, or UI-like output for a fresh-food result.
