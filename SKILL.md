---
name: literature-review-notes
description: "Personal literature review note workflow for engineering and AI papers. Use when the user uploads or references screenshots/photos of paper sections and asks to extract text, transcribe formulas, describe figures/tables, translate into Chinese, explain screenshot content, or break down explicit mathematical formulas for literature review notes. Supports numbered modes: 1 for screenshot reading, 2 for formula breakdown, and 1+2/1,2/1 and 2 style combinations."
---

# Literature Review Notes

## Overview

Use this skill to process screenshots or photos from engineering and AI research papers into clear note-ready text. The skill currently supports two numbered modes:

- `1`: Screenshot Reading Mode.
- `2`: Formula Breakdown Mode.

Do not try to produce a full literature review unless the user explicitly asks for it. Treat screenshots as partial evidence and avoid inventing missing paper context.

## Mode Selection

Use the user's numeric selection as the source of truth:

- `1`: Run Screenshot Reading Mode only.
- `2`: Run Formula Breakdown Mode only.
- `1+2`, `1,2`, `1 and 2`, or equivalent Chinese comma/list-separator variants: Run Screenshot Reading Mode first, then Formula Breakdown Mode.

The presence of formulas in an image does not automatically trigger Formula Breakdown Mode. If the user selects only `1`, transcribe and translate visible formulas as part of the screenshot reading workflow, but do not perform deep formula breakdown.

If the user does not provide a number but explicitly asks to break down, unpack, or explain a formula, run Formula Breakdown Mode. If the user asks generally to read, translate, or explain a paper screenshot, run Screenshot Reading Mode.

## Mode 1: Screenshot Reading

When the user provides a paper screenshot or photo, respond in this order:

1. **Original Transcription**
   - Transcribe visible original text in the image as faithfully as possible.
   - Preserve section headings, paragraph order, figure captions, table labels, references to equations, and visible citation markers.
   - Transcribe formulas with LaTeX-style notation when possible.
   - Keep original symbols, subscripts, superscripts, Greek letters, and operators.
   - For figures, diagrams, plots, tables, or model illustrations, describe the visible structure and labels in text.
   - Mark uncertain or unreadable parts explicitly with `[unclear]`, `[cropped]`, or `[not visible]`.

2. **Chinese Academic Translation**
   - Translate the transcribed content into Chinese.
   - Use accurate engineering, AI, machine learning, optimization, statistics, and mathematics terminology.
   - Keep key English terms in parentheses when the Chinese term may be ambiguous or the English term is standard in the field.
   - Preserve formulas and symbols rather than translating mathematical notation.
   - Preserve citation markers and equation/table/figure references.

3. **Chinese Explanation**
   - Explain the screenshot content in Chinese.
   - Clarify the role of formulas, variables, assumptions, modules, diagrams, or experimental details.
   - Explain why the content may matter for literature review notes: research problem, method, contribution, limitation, mechanism, evidence, or relation to prior work.
   - Clearly separate what is visible in the screenshot from reasonable interpretation.

### Output Format

Use these four Chinese headings exactly unless the user requests another format:

1. Yuanwen zhuanxie: use the Chinese heading meaning "original transcription".
2. Zhongwen fanyi: use the Chinese heading meaning "Chinese translation".
3. Zhongwen jieshi: use the Chinese heading meaning "Chinese explanation".
4. Buqueding zhichu: use the Chinese heading meaning "uncertainties".

Under the first heading, provide the visible original text, formulas, and figure/table descriptions.

Under the second heading, provide the Chinese academic translation.

Under the third heading, provide the Chinese explanation.

Under the fourth heading, list unreadable, cropped, ambiguous, or context-dependent items. If all content is clear, state in Chinese that there are no obvious uncertainties.

## Mode 2: Formula Breakdown

Use this mode only for explicit mathematical formulas visible in the screenshot, such as definitions, objective functions, loss functions, constraints, update rules, evaluation metric formulas, probability/statistics expressions, or equation steps in theoretical derivations.

Do not use this mode for ordinary flowcharts, purely textual mechanism descriptions, or pseudocode without mathematical expressions. If the user selects `2` but the screenshot contains no explicit mathematical formula, state that there is no explicit formula to break down and ask for a screenshot containing a formula.

For each formula, respond with the following sections in this order:

1. **Formula Transcription**
   - Transcribe the visible formula as faithfully as possible in LaTeX-style notation.
   - Preserve equation numbers, subscripts, superscripts, Greek letters, summations, integrals, expectations, norms, argmin/argmax, constraints, fractions, matrices, vectors, and set symbols when visible.
   - Mark unclear, cropped, or missing formula parts explicitly.

2. **Term-by-Term Explanation**
   - Explain what the left-hand side represents.
   - Explain each major right-hand-side term or component.
   - Explain the role of operators and structures such as addition, multiplication, fractions, summations, expectations, minimization, maximization, constraints, and normalization.
   - Prefer definitions visible in the screenshot. If a symbol is not defined in the screenshot, clearly label any explanation as an inference from common notation.

3. **Intuition**
   - Explain in Chinese what the formula is trying to express.
   - Focus on the reading intuition: what the formula measures, optimizes, constrains, defines, compares, or combines.
   - Avoid adding paper context that is not visible unless it is clearly labeled as a tentative inference.

4. **Formula Type**
   - Classify the formula when possible as one of: definition, objective function, loss function, constraint, update rule, evaluation metric, probability/statistics expression, intermediate derivation step, or other.
   - If the type cannot be determined from the screenshot, say why.

5. **Uncertainties**
   - List symbols that are unclear, cropped, undefined, or context-dependent.
   - List any explanation that depends on common notation rather than visible evidence.
   - State when more surrounding text, a previous page, or a following definition is needed.

### Multiple Formulas

If the screenshot contains multiple formulas, process them in equation-number order when equation numbers are visible; otherwise process them in reading order.

Use a separate block for each formula:

```markdown
# Formula 1

## 1. Formula Transcription

## 2. Term-by-Term Explanation

## 3. Intuition

## 4. Formula Type

## 5. Uncertainties
```

If multiple formulas have a visible relationship, add a final section explaining their relationship, such as definition-to-use, objective-to-constraint, derivation step, main formula plus auxiliary formula, or training objective versus evaluation metric.

## Terminology Preferences

Prefer standard Chinese academic translations in engineering and AI contexts for terms such as model, framework, architecture, representation, embedding, feature, objective function, loss function, optimization, constraint, inference, training, fine-tuning, dataset, benchmark, ablation study, evaluation metric, robustness, and generalization.

When a term has multiple plausible translations, include the English term in parentheses and briefly explain the choice if it affects interpretation.

## Accuracy Rules

- Do not fabricate text that is not visible.
- Do not silently repair incomplete equations; mark missing parts.
- Do not infer claims from surrounding paper sections that are not provided.
- Do not over-summarize before transcription; the user needs the original content first.
- Do not perform Formula Breakdown Mode unless the user selects `2` or explicitly asks for formula breakdown.
- If the image quality is too low, ask for a clearer image or a closer crop after providing whatever can be read.
- If there are multiple screenshots, process them in the user's given order and label each screenshot.

## Future Expansion Slots

This skill may later add workflows for literature matrices, paper comparison, citation extraction, theme synthesis, and long-form review drafting. Do not activate those workflows until their instructions are added.
