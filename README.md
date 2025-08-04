# News to Tweets: Stylized Headline Generation Using LLMs
This repository uses large language models to rewrite real-world news headlines into tweet-style messages using different tone and strategy combinations. Headlines were manually curated from trusted public sources.

---

## One Sentence Summary
This repository applies prompt-based generation using FLAN-T5 to convert news headlines into tweet-style outputs across multiple tones and strategies, evaluating both style and content preservation.

--- 

## Overview 

**Task**:
Convert a dataset of news headlines into tweet-formatted summaries that mimic realistic Twitter styles, such as "breaking news", "policy statements", or "funny takes".

**Approach**:  
Using the `google/flan-t5-base` model, we apply three prompt strategies (zero-shot, instruct, few-shot) and three tones (breaking, funny, policy). Each headline is rewritten using 9 tone-strategy pairs. We evaluate the outputs using two metrics:
- **Style Score**: Based on tweet features (length, hashtags, caps)
- **Entity Score**: Named Entity overlap with original headline using spaCy

**Performance Summary**:  
The best performance came from `funny + fewshot` with an average style score of 2.80 and entity score of 0.81. All generations were completed using prompt engineering only — no fine-tuning required.

---

## Summary of Work Done

### Data

- **Type**: New Headlines
- **Format**: CSV with a single column (`text`)
- **Size**: 30 samples
- **Split**: No train/test split needed (inference-only)
- **Preprocessing**: Minor cleaning for formatting and clarity

### Data Visualization 

We visualized: 
- Tweet length distributions by strategy
- Style scores across tone-strategy pairs
- Entity overlap trends

---

## Problem Formulation

- **Input**: News headline (string)
- **Output**: Stylized tweet (max 280 chars)
- **Model**: `google/flan-t5-base` via Hugging Face transformers
- **Prompt Strategies**:
    - **Zero-shot**: Direct instructions
    - **Instruct**: Slightly richer guidance
    - **Few-shot**: 2-3 examples in prompt
 
---

## Training 

- **Method**: Prompt-based generation (no model fine-tuning)
- **Enviroment**: Google Colab
- **Time**: ~1.5-2 minutes to generate all tweets variants
- **Issues**: Slow few-shot prompts, fixed with batching and simple loops

---

## Performance 
| Tone     | Strategy   | Avg Style Score | Avg Entity Score | Avg Tweet Length |
|----------|------------|------------------|------------------|------------------|
| funny    | fewshot    | 2.80             | 0.81             | 195              |
| breaking | instruct   | 2.56             | 0.76             | 170              |
| policy   | zero       | 2.03             | 0.60             | 125              |

---

## Conclusions 

- Few-shot prompting yields most tweet-like outputs
- Funny tone encourages better stylization
- Entity overlap is consistently higher with instruct-mode prompts

---

## Futute Work

- Add a second model (e.g., FLAN-T5-Large or Mistral)
- Fine-tune a dataset of real tweets
- Automatically suggest tone/strategy based on headline content

---

## How to Reproduce Results

1. Open `news_to_tweet-ipynb` in Colab or Jupyter
2. Upload `news_examples_30.csv`
3. Run the noteboo top-to-bottom
4. Download `final_llm_outputs.csv` and `summary_scores.csv`

No training required -- prompt-based inference only
