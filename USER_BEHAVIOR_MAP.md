# User Behavior Map

This document maps the expected user flow for `dog-fresh-food-helper`.

The skill is designed to help users move from “I want to cook something fresh for my dog” to a cautious, structured result. It must distinguish simple 10% add-ons from meal replacement or long-term homemade feeding, and it must not turn calorie matching into a claim of nutritional completeness.

## Core Flow

```mermaid
flowchart TD
    A[User invokes dog-fresh-food-helper] --> B{Dog profile available?}

    B -- Yes --> C[Summarize visible profile]
    C --> D{User confirms profile?}
    D -- Needs edits --> E[Collect missing or corrected profile fields]
    D -- Confirmed --> G[Risk gate]

    B -- No --> F[Collect compact dog profile in conversation]
    F --> G
    E --> G

    G{Healthy adult maintenance case?}
    G -- No / unclear --> H[Save profile context and give veterinary-gated guidance]
    H --> H1[Ask for professional confirmation or missing health details]

    G -- Yes --> I{Required data for energy estimate present?}
    I -- Missing weight/activity/body condition --> J[Ask only for missing fields]
    J --> I

    I -- Sufficient --> K[Estimate daily energy reference]
    K --> K1[Add data-source note and risk reminder]
    K1 --> L{User confirms activity/body condition/current stable intake?}
    L -- No --> J
    L -- Yes --> M[Classify feeding path]

    M --> N{Feeding path}

    N -- 10% add-on / occasional topper --> O[Calculate optional 10% calorie budget]
    O --> P[Check ingredients and group roles]
    P --> Q[Draft cautious add-on structure]
    Q --> R[Generate UI-style recipe card spec with pie/donut chart]
    R --> S[Output next confirmation question]

    N -- One-off single-meal replacement --> T{Nutrient analysis available?}
    T -- Yes --> U[Run nutrient-level analysis]
    U --> V[Show gaps/adequate/excess categories]
    V --> W[Generate cautious one-off result and UI card if appropriate]
    W --> S

    T -- No --> X[Do not fill meal by calories alone]
    X --> Y[List likely missing nutrient categories]
    Y --> Z[Ask to downgrade to 10% add-on or provide data for nutrient analysis]

    N -- Partial replacement above 10% --> AA{Nutrient analysis available?}
    N -- Transition plan --> AA
    N -- Long-term homemade feeding --> AA

    AA -- Yes --> U
    AA -- No --> AB[Block complete feeding plan]
    AB --> AC[Explain energy-balanced is not nutrient-balanced]
    AC --> Y
```

## First-Use Intake

```mermaid
flowchart LR
    A[Ask if profile already exists] --> B{Profile provided?}
    B -- Yes --> C[Summarize profile]
    B -- No --> D[Ask compact profile questions]

    D --> D1[Name / age / breed]
    D --> D2[Weight / body condition]
    D --> D3[Activity level]
    D --> D4[Current main food / meal frequency]
    D --> D5[Health flags / allergies / prescription diet]
    D --> D6[Fresh-food goal]

    C --> E[Ask user to confirm or correct]
    D1 --> E
    D2 --> E
    D3 --> E
    D4 --> E
    D5 --> E
    D6 --> E
```

## Path Gate

```mermaid
flowchart TD
    A[User describes ingredients or fresh-food goal] --> B{What is the intended use?}

    B -- Occasional topper --> C[10% add-on path]
    B -- Replace snack --> C
    B -- 10% fresh-food add-on --> C

    C --> D[Use calorie budget + ingredient safety checks]
    D --> E[May provide rough amount estimates if profile and data are sufficient]
    E --> F[Generate recipe UI card spec]

    B -- Replace one meal --> G[Single-meal replacement path]
    G --> H{Nutrient analysis available?}
    H -- Yes --> I[Analyze nutrients against NRC needs]
    H -- No --> J[Do not generate calorie-only full meal]

    B -- Above 10% fresh food --> K[Advanced feeding path]
    B -- Transition to fresh food --> K
    B -- Long-term homemade feeding --> K
    K --> L{Nutrient analysis available?}
    L -- Yes --> I
    L -- No --> M[Block complete plan and explain missing analysis]

    J --> N[List likely gaps: calcium/phosphorus, trace minerals, vitamins, fatty acids, variety]
    M --> N
    N --> O[Ask whether to downgrade to 10% add-on or provide full data]
```

## Output Decision Table

| User intent | Allowed output | Must not do |
| --- | --- | --- |
| Create dog profile | Ask compact questions, summarize known and unknown fields | Invent unknown profile data |
| Estimate daily intake | Provide NRC-style adult maintenance energy reference if healthy adult data is sufficient | Present energy estimate as a complete diet prescription |
| 10% add-on | Calculate calorie budget, check safety, group ingredients, provide rough plan and UI card | Say the meal is complete, balanced, or NRC-compliant |
| One-off meal replacement | Estimate calories and give cautious one-time structure only if boundaries are clear | Turn a few ingredients into a repeatable balanced template |
| Above 10% / transition / long-term homemade | Require nutrient-level analysis or block complete plan | Generate a recipe from calories alone |
| Nutrient analysis unavailable | List likely missing categories and ask for next step | Pretend the meal is nutritionally adequate |
| Recipe completed | Include data-source note, risk reminder, and UI-style recipe card with pie/donut chart | Force a phone-screen format or call the chart a scientific nutrition ratio |

## Final Recipe Card Flow

```mermaid
flowchart TD
    A[Recipe or ingredient plan is completed] --> B{Was result blocked by nutrient-analysis gate?}
    B -- Yes --> C[No UI card]
    C --> D[Ask for downgrade to 10% add-on or full analysis data]

    B -- No --> E[Create UI-style recipe card spec]
    E --> F[Header: title, dog name, date, path]
    E --> G[Ingredient share panel with pie/donut chart]
    E --> H[Complete ingredient list]
    E --> I[Separate supplement list]
    E --> J[Footer: data-source note + risk reminder]
    J --> K[Ask whether user wants an actual image/share card]
```

## Key Guardrails

- Ask for or confirm a dog profile before giving concrete food suggestions.
- Gate puppies, pregnancy/lactation, illness, prescription diets, allergies, gastrointestinal symptoms, obesity treatment, or unclear health status.
- Treat NRC-style daily intake as an energy estimate only.
- Keep 10% as a calorie budget, not a food-weight rule.
- Treat energy balance and nutrient balance as separate concepts.
- Require nutrient-level analysis for single-meal replacement if it is meant to be repeated, for above-10% fresh food, for transition plans, and for long-term homemade feeding.
- Include data-source notes and risk reminders whenever calculations or concrete plans appear.
- Use the UI card as an information summary, not as proof that the recipe is complete.
