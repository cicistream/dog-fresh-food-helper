# Dog Fresh Food Helper

A Codex skill for helping dog owners organize cautious cooked fresh-food ideas: create or confirm a dog profile, estimate adult maintenance energy, distinguish 10% add-ons from meal replacement, and keep nutrition-safety boundaries visible.

This skill is designed for “less guessing”, not for replacing a veterinarian, veterinary nutritionist, or a full recipe-analysis tool.

## What It Helps With

- Create or confirm a basic dog profile before giving food suggestions.
- Estimate daily energy intake for healthy adult maintenance cases using NRC-style logic.
- Separate common feeding paths:
  - 10% fresh-food add-ons or toppers;
  - one-off single-meal replacement;
  - partial replacement above 10%;
  - transition plans;
  - long-term homemade feeding.
- Group ingredients into practical roles: main protein, vegetables, small additions, and separate supplements.
- Add concise data-source notes and risk reminders whenever calculations or concrete food plans appear.
- Block calorie-only “full meal” answers when nutrient-level analysis is required.

## What It Does Not Do

This skill does not claim that a meal is complete, balanced, NRC-compliant, AAFCO-compliant, therapeutic, or suitable for long-term full feeding.

It also does not turn a few ingredients into a full homemade diet by matching calories. For meal replacement, higher fresh-food ratios, transition plans, or long-term homemade feeding, it requires nutrient-level analysis or clearly says the analysis cannot be completed yet.

## Core Safety Model

The skill uses a path gate before food planning:

| Path | What the skill may do |
| --- | --- |
| 10% add-on | Use calorie budget, ingredient safety checks, and cautious rough structure. |
| One-off meal replacement | Estimate calories and give a cautious one-time structure, while warning it is not a repeatable balanced template. |
| Above 10%, transition, or long-term homemade feeding | Require nutrient-level NRC analysis; if unavailable, stop short of a complete feeding plan. |

The key rule is:

```text
Energy-balanced is not nutrient-balanced.
```

Calories answer how much energy a meal provides. They do not prove calcium/phosphorus balance, trace minerals, vitamins, essential fatty acids, amino acid adequacy, or safe upper-limit control.

## Data Notes

When calculations appear, the skill should briefly say what kind of data is being used:

- NRC-style energy logic for daily maintenance calorie estimates;
- public food composition data for generic ingredients;
- package label data for commercial foods, supplements, or branded products;
- user-provided values when exact ingredient data is unavailable.

Food data is approximate. Ingredient variety, brand, batch, cooked/raw state, cooking loss, and weighing method can all change the result.

## Installation

Clone this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/cicistream/dog-fresh-food-helper.git ~/.codex/skills/dog-fresh-food-helper
```

If the skill already exists locally, update it with:

```bash
cd ~/.codex/skills/dog-fresh-food-helper
git pull
```

## Usage

In Codex, ask for help with a dog fresh-food plan. The skill can be invoked automatically when the request matches, or explicitly:

```text
$dog-fresh-food-helper
我想给狗狗做一顿熟制鲜食，先帮我建立档案并判断这是加餐还是替代一顿。
```

Example first-use prompt:

```text
我家狗狗叫啾啾，1 岁，马尔泰，2.5kg，绝育，普通活跃，主食是狗粮，没有疾病史。今晚想用牛肉、黄瓜、西红柿做鲜食。
```

The skill should first clarify whether this is a 10% add-on, a one-off meal replacement, or a repeatable homemade-feeding path before giving amounts.

## Repository Structure

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── fresh-food-boundaries.md
    ├── initial-profile-prompt.md
    ├── nrc-energy-estimate.md
    └── nutrient-analysis-gate.md
```

## References Inside The Skill

- `references/initial-profile-prompt.md`: reusable first-use flow and profile template.
- `references/nrc-energy-estimate.md`: adult maintenance energy estimate rules and risk wording.
- `references/fresh-food-boundaries.md`: wording and safety boundaries for fresh-food helper responses.
- `references/nutrient-analysis-gate.md`: rules for meal replacement, above-10% fresh food, and nutrient-analysis gating.

## Disclaimer

This skill is for cautious self-use planning and communication. It is not veterinary advice, not a diagnostic tool, and not a complete diet formulation engine. For illness, prescription diets, allergies, gastrointestinal symptoms, weight treatment, puppies, pregnancy/lactation, or long-term homemade feeding, consult a veterinarian or veterinary nutritionist.
