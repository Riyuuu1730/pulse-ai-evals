# pulse-ai-evals
AI evals project on Pulse by Nova, a fictional AI support agent: rubric, golden dataset, human review and LLM as a judge.
Pulse by Nova — An AI Evals Case Study

How would a product manager evaluate an AI agent before shipping it? This is a hands-on answer: I built a fictional AI support agent, then ran a full evaluation on it — a rubric, a golden dataset, human review, and an LLM acting as a judge.

The product: Pulse by Nova, a fictional AI agent that answers SAP support tickets (locked accounts, failed transports, slow systems). The method: 17 test cases / 32 answers, each scored by me against a 5-part rubric, then re-scored by an LLM judge. The headline result: a blind LLM judge agreed with my expert verdict only 46% of the time. After I taught it my failure rules, agreement rose to 82%.

Independent learning project. Pulse and Nova are fictional. Inspired by AI agents like Spark (Nexthink) and Joule (SAP), but not affiliated with and making no claims about either. No real company data was used.

Why this project

A general benchmark score tells you how smart a model is. It does not tell you whether your product does what your users need. That gap is what product evals close — they turn a product manager's judgement of "good" into something measurable, so every change can be tested instead of guessed.

I come from an SAP background, so I know what a good support answer looks like in that world. I used that to ask a product question: if I owned an agent like Spark or Joule, how would I decide it was ready to ship?

What I did

1. Defined the rubric. Before testing anything, I wrote down what a good answer means for this product. Every answer is scored on five things:

Criterion	The question it answers
Product knowledge	Does it understand the problem and read the system data correctly?
Policy compliance	Does it stay within what it is allowed to do?
Decision making	Does it fix what it can and escalate what it must, safely?
Priority	Does the urgency match the business impact?
Tone	Is the message clear for a business user?

Each answer is graded PASS / WEAK PASS / FAIL.

2. Built a golden dataset. 17 realistic test cases (32 answers across multi-turn conversations), grouped by problem area: account lockouts, transports to production, system health, security attacks, reporting, and out-of-scope requests. The cases include deliberate traps — a fake approval note, a four-turn social-engineering attack, and a HANA failover that a real expert would catch early.

3. Human review (Level 2 eval). I read and scored all 32 answers against the rubric, with a written critique for each. This is where the real findings came from — for example, the agent often decided before investigating, and mis-judged urgency on the biggest incidents.

4. LLM as a judge. To make this scale, I had an LLM re-score every answer. I ran it twice:

Blind (rubric only) → agreed with me on 46% of verdicts, and was fooled by the same fake approval note the agent should have caught.
Calibrated (my failure rules + a few of my scored examples added to the judge) → agreement rose to 82%, and dangerous misses dropped.

5. Iterated the product. Four versions of the agent's prompt. The worst failure (unlocking an account on an assumption) was fixed between versions.

Key takeaways
Every AI product needs evals — without them, every change is a guess.
A domain expert is essential — the human defines what "good" means. A blind AI judge could not catch what an expert could.
Evals never stop — test, fix, and test again after every change.


What's in this repo
Folder	File	What it is

1_product/	Pulse_by_Nova_PRD.md	The product requirements for the agent
2_prompts/	Pulse_Prompts.pdf	The agent's system prompts, all versions
3_dataset_and_rubric/	Pulse_Golden_Dataset.xlsx	The rubric, all 32 scored answers, and the judge comparison
4_llm_judge/	Pulse_LLM_Judge_Kit.txt	The blind judge prompt and batches
4_llm_judge/	Pulse_Calibrated_Judge_Kit.txt	The calibrated judge prompt
4_llm_judge/	Pulse_Judge_Results.csv / Pulse_Calibrated_Judge_Results.csv	Both judges' raw scores
5_results/	Pulse_Evals_Case_Study.pdf	The full written case study
6_slides/	Pulse_AI_Evals_Carousel.pdf	The summary slides

Tools used
Built in Google AI Studio (Gemini). Evaluation tracked in Excel, the way the approach's authors recommend starting. The LLM judge was run in ChatGPT.

Next step: as a product like this gets real users, the evaluation would move from a spreadsheet to a tracing tool such as Arize Phoenix or LangSmith, to capture and score live conversations at scale.

Credit

The evaluation method follows the work of Hamel Husain and Shreya Shankar on AI evals (their guides).

Riya Murdia · AI Product Owner
