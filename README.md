# Class Stuck Topics

Which topics is *this* class stuck on, and how early can you tell?

Teachers can't read hundreds of AI-tutor conversations. This notebook tests whether a class-level "stuck topic" signal can be computed from the first few problems students do, using real classroom data.

## Data
ASSISTments 2009-2010 skill builder dataset (corrected, collapsed): middle-school math practice from 4,151 students across 245 classes and 101 skills. Download `skill_builder_data_corrected_collapsed.csv` from the ASSISTments datasets page and place it next to the notebook.

## Setup
- A student **masters** a skill after 3 correct answers in a row (ASSISTments' skill-builder rule).
- A class is **stuck** on a skill when at least half of its students never master it (class-skill pairs with 5+ students).
- Signals use only each student's **first k problems** on the skill.
- Cross-validation is grouped by class, so no class appears in both train and test folds.

## Findings
| Signal | AUC | Precision in top 20% flagged |
|---|---|---|
| Topic difficulty (from other classes) | 0.73 | 53% |
| This class's % correct (first 3 problems) | 0.84 | 61% |
| Both combined | **0.88** | **63%** |

Base rate: 22% of class-topics are stuck.

- **Stuck depends on the class, not just the topic.** Of 70 skills taught in 5+ classes, 84% are stuck in some classes and fine in others. A fixed "hard topics" list misses this.
- **The signal shows up early.** With just one problem per student, AUC is 0.82. It reaches 0.88 by 3 problems and 0.89 by 5.
- **Hints and retries add nothing** at the class level once % correct is known.

## What it suggests for AI-tutor products
Rank topics per class by early struggle so teachers know where to step in before reading transcripts. Tutor conversations could sharpen this further with signal practice data lacks, such as stated confusions.

## Caveats
2009-2010 middle-school math. "3 in a row" is one mastery rule among many. Students who stop early may look unmastered for other reasons.

## Run
pip install pandas numpy scikit-learn matplotlib
jupyter notebook class_stuck_topics.ipynb

Jahangir Mammadli · [mammadli.dev](https://mammadli.dev)
Data: ASSISTments (Feng, Heffernan & Koedinger, 2009)
