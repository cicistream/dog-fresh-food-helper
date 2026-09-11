---
name: dog-fresh-food-helper
description: Help create or confirm a basic dog profile, estimate daily energy intake from NRC-style adult maintenance logic, and plan occasional cooked fresh-food add-ons with conservative safety boundaries. Use for profile intake, conversational confirmation, ingredient grouping, rough structure checks, and owner-facing safety notes; do not use as a veterinary diagnosis tool or complete diet formulation tool.
---

# Dog Fresh Food Helper

Use this skill when the user wants help turning a dog profile and fresh-food idea into a cautious, readable structure: basic dog context, NRC-style daily energy estimate, ingredient groups, visible risks, preparation reminders, and owner-facing caveats.

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
6. **Food planning**: Only after the profile and daily energy reference are confirmed, review ingredients or draft a fresh-food structure.

Ask only for details needed to assess broad suitability and risk:

1. dog name, age or life stage, breed, sex/neuter status;
2. current weight and approximate body condition;
3. daily activity level;
4. current main food and meal frequency;
5. known illnesses, prescription diets, allergies, intolerances, or recent digestive symptoms;
6. fresh-food goal: occasional topper, partial replacement, transition plan, or long-term full homemade feeding.

After a profile exists, summarize it as “狗狗档案” and clearly mark unknown fields instead of inventing them. If enough healthy-adult data exists, include “每日能量摄入参考” and explain the estimate source briefly.

## Default Output

When asked to review or draft a fresh-food helper result, structure the answer as:

1. **一句话判断**: whether the idea is suitable as an occasional add-on, needs adjustment, or should be veterinary-gated.
2. **狗狗档案影响**: what the known profile changes, and what is still unknown.
3. **每日能量参考**: NRC-style adult maintenance estimate if appropriate, plus the optional fresh-food add-on energy budget when relevant. Say clearly that 10% means calories, not food weight.
4. **食材分层**:
   - 主体食材: usually cooked lean animal protein.
   - 蔬菜搭配: dog-safe vegetables prepared plainly.
   - 少量搭配: egg, organ meat, seeds, fruit, or other small additions.
   - 日常补充: supplements, if any, listed separately and not hidden inside the food ratio.
5. **需要注意**: toxic foods, seasoning, fat level, new-food tolerance, choking/texture, storage, or missing calcium/completeness caveats.
6. **数据来源提示**: one short sentence describing whether values come from NRC-style energy logic, public food composition data, package labels, or user-provided numbers.
7. **风险提醒**: one short caveat whenever the answer includes calculation or a concrete plan.
8. **下一步确认**: one concise question that moves the user forward, such as confirming planned calories, meal frequency, whether this is an occasional add-on, or whether they want to record today's ingredients.

## Important Rules

- “10%” means calories, not food weight. Do not present a plate ratio as a scientific standard.
- NRC-style daily intake output is an energy estimate for adult maintenance, not a guarantee that the food is complete or balanced.
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
