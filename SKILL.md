---
name: literature-review-notes
description: Personal literature review note workflow for engineering and AI papers. Use when the user uploads or references screenshots/photos of paper sections and asks to extract text, transcribe formulas, describe figures/tables, translate into Chinese, or explain the screenshot content for literature review notes. Trigger on requests such as "paper screenshot", "literature review notes", "transcribe this image", "translate and explain this paper section", "extract the formula from this screenshot", or Chinese requests about processing paper screenshots.
---

# Literature Review Notes

## Overview

Use this skill to process screenshots or photos from engineering and AI research papers into a clear note-ready text response. The first version focuses on one workflow: image content transcription, Chinese academic translation, and Chinese explanation.

Do not try to produce a full literature review unless the user explicitly asks for it. Treat screenshots as partial evidence and avoid inventing missing paper context.

## Default Workflow

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

## Output Format

Use these four Chinese headings exactly unless the user requests another format:

1. Yuanwen zhuanxie: use the Chinese heading meaning "original transcription".
2. Zhongwen fanyi: use the Chinese heading meaning "Chinese translation".
3. Zhongwen jieshi: use the Chinese heading meaning "Chinese explanation".
4. Buqueding zhichu: use the Chinese heading meaning "uncertainties".

Under the first heading, provide the visible original text, formulas, and figure/table descriptions.

Under the second heading, provide the Chinese academic translation.

Under the third heading, provide the Chinese explanation.

Under the fourth heading, list unreadable, cropped, ambiguous, or context-dependent items. If all content is clear, state in Chinese that there are no obvious uncertainties.

## Terminology Preferences

Prefer standard Chinese academic translations in engineering and AI contexts for terms such as model, framework, architecture, representation, embedding, feature, objective function, loss function, optimization, constraint, inference, training, fine-tuning, dataset, benchmark, ablation study, evaluation metric, robustness, and generalization.

When a term has multiple plausible translations, include the English term in parentheses and briefly explain the choice if it affects interpretation.

## Accuracy Rules

- Do not fabricate text that is not visible.
- Do not silently repair incomplete equations; mark missing parts.
- Do not infer claims from surrounding paper sections that are not provided.
- Do not over-summarize before transcription; the user needs the original content first.
- If the image quality is too low, ask for a clearer image or a closer crop after providing whatever can be read.
- If there are multiple screenshots, process them in the user's given order and label each screenshot.

## Future Expansion Slots

This skill may later add workflows for literature matrices, paper comparison, citation extraction, theme synthesis, and long-form review drafting. Do not activate those workflows until their instructions are added.
