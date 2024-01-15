# Machine-Translation-of-code-mixed-Hindi-English-Text-to-English-with-mBART

This project is implemented in Summer Internship at IIIT Surat, under the guidance of [Dr Pradeep Kumar Roy](https://www.linkedin.com/in/pradeep-kumar-roy-49133995) from June 2022 to August 2022.

In this project I've:
- Developed sequence to sequence models for Machine Translation.
- Created a text mapping of 200 most common words in English and Hindi and implemented Text Normalization for multi-lingual (2 languages) data (Hindi and English) to correct the misspelled words.
- Performed the translation using mBART (Hugging Face Transformers), achieved a Bilingual Evaluation Understudy (BLEU) score more than 30.

### About the Dataset

- ```English-Hindi code-mixed parallel corpus.csv``` contains a code-mixed text and it's corresponding English Translation
- ```norm_words.json``` contains text mappings for most common words in English and Hindi to correct the misspelled words.

### Text Normalization

  Text normalization is the process of transforming text into a single standard
form that it might not have had before. Normalizing text before storing or
processing it allows for separation of concerns, since input is guaranteed to be
consistent before operations are performed on it.
Text normalization requires being aware of what type of text is to be
normalized and how it is to be processed afterwards; there is no all-purpose
normalization procedure. It completely depends on the text that is being processed.
For this task a Hindi-English Code mixed (Hinglish) corpus is created in
which for each sample a complete English Translation is also created. The purpose
of the task is to correct the words in Hinglish corpus with their original word (ex:
hai - hain, gd -good, etc). A Json file is created (which can be loaded as a
dictionary later) for the wrong spelt words with their correct spelling.
The following images shows the difference between original text and text
after correction in the Hinglish corpus:

![Capture](https://user-images.githubusercontent.com/68743810/216002289-1c151c02-0345-40be-8393-7de1c2a4b71c.PNG)

### Applying mBART and Google Translator API and comparing results

  The mBart model was presented in Multilingual Denoising Pre-training for
Neural Machine Translation by Yinhan Liu, Jiatao Gu, Naman Goyal, Xian Li,
Sergey Edunov Marjan Ghazvininejad, Mike Lewis, Luke Zettlemoyer.
According to the abstract, MBART is a sequence-to-sequence denoising
auto-encoder pretrained on large-scale monolingual corpora in many languages
using the BART objective. mBART is one of the first methods for pretraining a
complete sequence-to-sequence model by denoising full texts in multiple
languages, while previous approaches have focused only on the encoder, decoder,
or reconstructing parts of the text.
  
  “Multilingual translation models can be created through multilingual
finetuning. Instead of fine tuning in one direction, a pre-trained model is finetuned
in many directions at the same time. It demonstrates that pretrained models can be
extended to incorporate additional languages without loss of performance.
Multilingual finetuning improves on average 1 BLEU over the strongest baselines
(being either multilingual from scratch or bilingual finetuning) while improving
BLEU on average over bilingual baselines from scratch.” (from abstract)

  The corrected sentences in the previous task are passed to google
transliteration which generates text in pure hindi, as the pre-trained mBART model
was trained on hindi texts. Then the texts were passed to pre-trained mBART and
the predictions were made. The following are some outputs of the predicted
samples:

![Capture_1](https://user-images.githubusercontent.com/68743810/216003112-4546aaa1-9ede-470d-879b-aa57acd87949.PNG)

![Capture_2](https://user-images.githubusercontent.com/68743810/216003221-48399dc6-8dbc-4966-9771-b1f5b5790d54.PNG)

And then the same samples were also tested against Google Translate API
and BLEU Score was evaluated in both the cases.

BLEU (BiLingual Evaluation Understudy) is a metric for automatically
evaluating machine-translated text. The BLEU score is a number between zero and
one that measures the similarity of the machine-translated text to a set of high
quality reference translations. A value of 0 means that the machine-translated
output has no overlap with the reference translation (low quality) while a value of 1
means there is perfect overlap with the reference translations (high quality).

![Capture_3](https://user-images.githubusercontent.com/68743810/216004121-6f2a6a6f-1b19-4df8-bf5e-8ce64dad0a0f.PNG)

The BLEU Score for mBART model’s prediction with Original Translation is
30.88047790468621 and using Google Translate API (SOTA model) it is
47.996668017519724.
