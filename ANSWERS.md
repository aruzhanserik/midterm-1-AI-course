# Midterm 1: answers

GitHub username: `aruzhanserik`
Session code: `maple-66`
Fingerprint: `6fb0f779`

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I used Python to run the code and obtain the results from my dataset. I reviewed the outputs and checked the calculations to make sure they matched the required formulas. When I had difficulties understanding some concepts I used AI assistance to help clarify them. 

I used Gemini to help check my Python code for processing the provided datasets and calculating the required metrics. I also used it to proofread my writing, correct grammar, and if needed make my explanations clearer to understand. The answers, reasoning, and final decisions in this submission are my own. 

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
| A, k=3 |17282 |
| A, k=5 |22264 |
| B, k=3 |11933 |
| B, k=5 |13349 |

### 1d. Decision (at most 150 words)

Chosen candidate: (B, 3)

Config A is out: (A,3) costs $17282 and (A,5) $22264, both over the $15300 budget. 
Two candidates fit: (B,3) at $11933 and (B,5) at $13349. 
Recall is 46.7 % [34.6–59.1] for (B,3) and 51.7 % [39.3–63.8] for (B,5). The intervals overlap, so (B,5) is not shown to be better, and paying $1416 more per year for an unproven gain is unreasinable. 
Recall of (B,3): EN 40 % (8/20, [21.9–61.3]), RU 60 % (12/20, [38.7–78.1]), KK 40 % (8/20, [21.9–61.3]). 
English and Kazakh users are served worst, but with 20 questions per language the intervals overlap, so no language is shown to differ. 
Overall, about half of the questions miss the right chunk at k=3.


### 1e. Next measurement (at most 60 words)
Re-measure recall@3 and recall@5 of config B on at least 300 real questions per language. If the (B,5) interval then lies above (B,3) the extra $1,416 a year is justified and switch will most likely happen, if not then (B,3) will stay.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.889 (160/180) |KK, degraded |0.667(20/30) |0.488 |0.808 |$59305 |
| L |0.800 (144/180) |KK, degraded |0.667(20/30) |0.488 |0.808 |$7200 |

Personal-data pages per year sent abroad under H:

### 2b. Memo (at most 300 words)
My choice is pipeline L.

**Who is served worst.** For both pipelines, the worst group is Kazakh scans in bad condition (degraded). Only 20 of 30 are correct, which is 66.7 %. The 95 % interval is 48.8 % to 80.8 %. The overall numbers (H 88.9 %, L 80.0 %) hide this problem, because the good groups make the average look better. About one in three bad Kazakh invoices fails. We tested only 30 invoices per group, so the interval is wide. I cannot say that H and L are really different in this group.

**Personal data.** 21 % of the pages have a person's name and ИИН. Kazakhstan's law No. 94-V covers the ИИН. With H, 613200 pages a year would leave the country. Three questions:
- Where does the scan go? H: to a data centre abroad. L: to our own server in Kazakhstan.
- Who stores it? H: the vendor, but I do not know the details, so I must ask for the contract. L: our bank.
- For how long? H: I do not know the vendor's retention time, so I must find out. L: we decide.

A vendor saying "we are safe" is not a compliance check.

**Safeguards we can check.**
- Delete scans and results from L after 30 days and keep a deletion log.
- Keep a list of who can open the data, and review the access log every 3 months.
- Block internet traffic going out from the server and test it.
- Send bad Kazakh scans and low-confidence results to a person, and count how many each month.

**My choice:** L costs $7200 a year. H costs $59305. With L, no ИИН leaves the country. The price is 8.9 points lower overall accuracy. 
The risk that remains: L will make more mistakes, and they are only caught if the human check works. If our server is hacked, that is our problem.


## Part 3: Explain your own numbers

### Q1

Number: 1.58
Why (at most 40 words): Bytes grow 2.12x but tokens 3.36x. Encoding explains only part of the Kazakh premium, the tokenizer adds a further 1.58x by splitting Kazakh into many more pieces, which makes the token ratio higher.


### Q2

Number: 503
Why (at most 40 words): A 576-token chunk is about 592 e5 tokens, but e5 reads only 512(limit). The sentence starts at 503, so almost all is cut. The question likely cannot retrieve this chunk, and no error appears because truncation is silent.


### Q3

Number: 92.7
Why (at most 40 words): The ranking stays the same, softmax keeps the order. Low Temperature only makes the top token much more likely. Every token still has a probability above zero, so none is removed, only top-p or top-k would cut tokens.


### Q4

Number: 12
Why (at most 40 words): The leaderboard prefers X (74 vs 70), because it has more correct answers, "I don't know" gets zero. That teaches models to always guess instead of admitting not knowing, which makes confident wrong answers (model hallucinations).


### Q5

Number: 9945
Why (at most 40 words): The first message is paid for 17 times by the last turn, once per turn. Prompt caching can make repeated tokens cheaper, even though the prompt is still used.