# LocQA: Localized Question Answering Benchmark

This repository contains the dataset for the paper **Location Not Found: Exposing Implicit Local and Global Biases in Multilingual LLMs** (ACL 2026).

**LocQA** is a diagnostic benchmark designed to probe the implicit priors of multilingual Large Language Models (LLMs). It evaluates how models resolve ambiguity in *locale-ambiguous* questions: queries where the factual answer depends entirely on the geographic location of the speaker (e.g., "What is the legal drinking age?" or "When does the fiscal year start?").

By analyzing which regional reality the model defaults to when the context is underspecified, LocQA maps models' implicit priors and hierarchy of representation.

## Dataset Statistics

* **Total Items:** 2,156 locale-specific questions and answers
* **Unique Templates:** 44 semantically parallel, locale-ambiguous questions 
* **Languages:** 12 (English, Spanish, French, German, Hebrew, Hindi, Indonesian, Italian, Japanese, Korean, Portuguese, Chinese)
* **Locales (Regions):** 49 distinct countries/regions
* **Domains Covered:** Holiday and Calendar, Law, Leisure and Culture, State and Country, Language

## Data Structure (`locqa.json`)

The dataset is provided in a single JSON file. The top-level keys are the English source question templates. Each entry contains the question's category and a breakdown of translations and region-specific ground-truth answers for every evaluated language.

### Schema Example

```json
{
  "What is the first workday of the week?": {
    "category": "Holiday and Calendar",
    "languages": {
      "English": {
        "translated_question": "What is the first workday of the week?",
        "answers": {
          "USA": "Monday",
          "UK": "Monday",
          "Canada": "Monday"
        }
      },
      "Hebrew": {
        "translated_question": "מהו יום העבודה הראשון בשבוע?",
        "answers": {
          "Israel": "ראשון"
        }
      }
    }
  }
}
```

### Key Fields:

* `category`: The topical domain of the question.
* `translated_question`: The localized, natural phrasing of the question in the target language. Translators preserved semantic ambiguity so that the target country is never explicitly named in the prompt.
* `answers`: A dictionary mapping valid countries/locales to their factual ground-truth answers. Note that some questions may have an `"N/A"` answer for specific locales if the concept does not exist there or the question is inapplicable.

## Citation

TBA
