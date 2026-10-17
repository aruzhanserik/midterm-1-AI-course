# Midterm 1: answers

GitHub username: `aruzhanserik`
Session code: `maple-66`
Fingerprint: `6fb0f779`

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.450 |0.500 |0.583 |0.493 |
| B |0.400 |0.467 |0.517 |0.457 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.500 |0.377 |0.623 |
| A, k=5 |0.583 |0.457 |0.699 |
| B, k=3 |0.467 |0.346 |0.591 |
| B, k=5 |0.517 |0.393 |0.638 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 |$17,282 |
| A, k=5 |$22,264 |
| B, k=3 |$11,933 |
| B, k=5 |$13,349 |

### 1d. Decision (at most 150 words)

Chosen candidate: (B, 3)

Config A is out: (A,3) costs $17,282 and (A,5) $22,264, both over the $15,300 budget. 
Two candidates fit: (B,3) at $11,933 and (B,5) at $13,349. Recall is 46.7 % [34.6–59.1] for (B,3) and 51.7 % [39.3–63.8] for (B,5). The intervals overlap, so (B,5) is not shown to be better, and paying $1,416 more per year for an unproven gain is unreasinable. Recall of (B,3): EN 40 % (8/20, [21.9–61.3]), RU 60 % (12/20, [38.7–78.1]), KK 40 % (8/20, [21.9–61.3]). 
English and Kazakh users are served worst, but with 20 questions per language the intervals overlap, so no language is shown to differ. Overall, about half of the questions miss the right chunk at k=3.


### 1e. Next measurement (at most 60 words)

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | | | | | | |
| L | | | | | | |

Personal-data pages per year sent abroad under H:

### 2b. Memo (at most 300 words)

## Part 3: Explain your own numbers

### Q1

Number:
Why (at most 40 words):

### Q2

Number:
Why (at most 40 words):

### Q3

Number:
Why (at most 40 words):

### Q4

Number:
Why (at most 40 words):

### Q5

Number:
Why (at most 40 words):
