Legal Document Summarization

A beginner-friendly notebook that summarizes legal contracts (NDAs and SLAs) using both extractive and abstractive summarization techniques, then evaluates the results with a custom clause-coverage metric.

What it does
Loads legal contracts from the CUAD (Contract Understanding Atticus Dataset), which contains real contracts with labeled clauses (e.g. Confidentiality, Indemnification).
Cleans and prepares the contract text for summarization.
Extractive summarization — pulls out the most important existing sentences using LexRank (via sumy).
Abstractive summarization — generates new summary text using a pre-trained transformer model (BART).
(Optional) Fine-tuning — shows how to fine-tune a summarization model on custom data.
Evaluation — scores summary quality using ROUGE, plus a custom "clause coverage" metric that checks whether key legal clause types are mentioned in the summary.
Comparison — runs both methods across a sample of contracts and compares average clause coverage side by side.
Why clause coverage?

Standard metrics like ROUGE measure text overlap with a reference summary, but legal summaries need to be reliable in a different way — they need to actually mention the clauses that matter (confidentiality terms, indemnification, termination conditions, etc.). This notebook's clause-coverage check flags when a summary silently drops an important clause type, which is the kind of omission that matters most in a legal context.

Requirements
bash
pip install -U transformers datasets sumy evaluate rouge_score nltk

A GPU is optional — the notebook detects and uses CUDA if available, and falls back to CPU otherwise.

Usage

Open legal_doc_summarization_b.ipynb in Jupyter and run the cells in order, from top to bottom. Each cell is documented with comments explaining what it does and why.

Notebook structure
Step	What happens
1	Install dependencies and check for GPU
2	Load the CUAD contract dataset
3	Clean and prepare contract text
4	Extractive summarization (LexRank)
5	Abstractive summarization (BART)
6	Optional fine-tuning on custom data
7	Clause coverage scoring
8	Summarize and compare a sample of contracts
Results

The notebook prints average clause coverage for each method (extractive vs. abstractive) across the sampled contracts, plus a full side-by-side example so you can read both summary styles directly.

Limitations & next steps
The fine-tuning step (Step 6) uses placeholder training data — swap in real, lawyer-written summaries for meaningful results.
Try t5-small or t5-base as an alternative to BART and compare quality.
Add proper ROUGE scoring in Step 8 once real reference summaries are available.
This is not a substitute for legal review. Abstractive summaries can subtly shift meaning; always have a qualified professional verify anything used for real decisions.
License

Add a license of your choice (e.g. MIT) before publishing.
