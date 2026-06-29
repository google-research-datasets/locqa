# LocQA: Localized Question Answering Benchmark

This repository contains the dataset for the paper [**Location Not Found: Exposing Implicit Local and Global Biases in Multilingual LLMs**](https://aclanthology.org/2026.acl-long.1344/) (ACL 2026).

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

```
@inproceedings{mor-lan-etal-2026-location,
    title = "Location Not Found: Exposing Implicit Local and Global Biases in Multilingual {LLM}s",
    author = "Mor-Lan, Guy  and
      Goldman, Omer  and
      Eyal, Matan  and
      Gilady, Adi Mayrav  and
      Eiger, Sivan  and
      Szpektor, Idan  and
      Hassidim, Avinatan  and
      Matias, Yossi  and
      Tsarfaty, Reut",
    editor = "Liakata, Maria  and
      Moreira, Viviane P.  and
      Zhang, Jiajun  and
      Jurgens, David",
    booktitle = "Proceedings of the 64th Annual Meeting of the {A}ssociation for {C}omputational {L}inguistics (Volume 1: Long Papers)",
    month = jul,
    year = "2026",
    address = "San Diego, California, United States",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.acl-long.1344/",
    pages = "29130--29150",
    ISBN = "979-8-89176-390-6",
    abstract = "Multilingual large language models (LLMs) have minimized the fluency gap between languages. This advancement, however, exposes models to the risk of biased behavior, as knowledge and norms may propagate across languages. In this work we aim to quantify models' inter- and intra-lingual biases, via their ability to answer locale-ambiguous questions. To this end, we present LocQA, a test set containing 2,156 questions in 12 languages, referring to various locale-dependent facts such as laws, dates, and measurements. The questions do not contain indications of the locales they relate to, other than the querying language itself. LLMs' responses to LocQA locale-ambiguous questions thus reveal models' implicit priors. We used LocQA to evaluate 32 models, and detected two types of structural biases. Inter-lingually, we show a global bias towards answers relevant to the US-locale, even when models are asked in languages other than English. Moreover, we discovered that this global bias is exacerbated in models that underwent instruction tuning, compared to their base counterparts. Intra-lingually, we show that when multiple locales are relevant for the same language, models act as demographic probability engines, prioritizing locales with larger populations. Taken together, insights from LocQA may help in shaping LLMs' desired local behavior, and in quantifying the impact of various training phases on different kinds of biases."
}
```
