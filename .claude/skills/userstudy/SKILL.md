---
name: userstudy
description: "[PM Twin] Generate user research plan and interview script from PRD — discovery, usability, or feedback studies."
argument-hint: "[discovery | usability | feedback]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, WebSearch
---

# User Study — Research Plan Generator

Generate user research plans and interview scripts based on the product's PRD and stage.

## Study Types

| Type | When | Goal |
|------|------|------|
| `discovery` | Before/during Phase 0 | Validate problem exists, understand user needs |
| `usability` | After MVP built | Test if users can complete key tasks |
| `feedback` | After launch | Gather user satisfaction, feature requests, pain points |

## Execution Steps

1. **Read PRD** — Target users, pain points, features, value prop
2. **Select study type** — discovery, usability, or feedback
3. **Research best practices** — WebSearch for "[domain] user research methods"
4. **Generate plan** — methodology, sample size, timeline, recruitment
5. **Generate script** — intro, warm-up, core questions, probes, wrap-up
6. **Save** — `docs/toolkit/research/[type]-plan.md` and `[type]-script.md`

## Output: Research Plan

```markdown
# [Type] Research Plan — [Product Name]

## Objective
[What we want to learn]

## Methodology
[Interviews / surveys / usability tests / diary studies]

## Participants
- Target: [user persona from PRD]
- Sample size: [5-8 for qualitative, 30+ for quantitative]
- Recruitment: [where to find them]
- Screening criteria: [must have / must not have]

## Timeline
| Step | Duration | When |
|------|----------|------|
| Recruitment | 1 week | Week 1 |
| Sessions | 1-2 weeks | Week 2-3 |
| Analysis | 3-5 days | Week 3-4 |
| Report | 2 days | Week 4 |

## Analysis Framework
- Themes to look for: [from PRD pain points]
- Success criteria: [from PRD acceptance criteria]
- Key questions to answer: [from PRD open questions]
```

## Output: Interview Script

```markdown
# [Type] Interview Script

## Setup (2 min)
- Thank participant
- Explain purpose (no wrong answers)
- Ask permission to record

## Warm-Up (3 min)
- "Tell me about your role / how you currently [do the thing]"
- "What tools do you use today?"

## Core Questions (20-30 min)
[5-8 open-ended questions tied to PRD pain points and features]

## Probes (as needed)
- "Can you tell me more about that?"
- "What would happen if you couldn't do that?"
- "How important is that on a scale of 1-10?"

## Wrap-Up (5 min)
- "Anything else I should know?"
- "Would you be open to a follow-up?"
- Thank and next steps
```

## Important Rules

- **Questions from the PRD** — every core question ties to a PRD pain point or feature
- **Open-ended questions** — never lead the participant
- **Realistic timelines** — don't promise results in a day
- **Ethical** — always note: informed consent, right to withdraw, data handling
