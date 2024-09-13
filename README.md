# Sign Language Datasets

**Datasets used by the <kbd>[sign_language_translator](https://github.com/sign-language-translator/sign-language-translator)</kbd> python package.**

| **Support Us** ❤️ | <!-- [![Stripe](https://img.shields.io/badge/Stripe-626CD9?logo=Stripe&logoColor=white)]() --> [![PayPal](https://img.shields.io/badge/PayPal-00457C?logo=paypal&logoColor=white)](https://www.paypal.com/donate/?hosted_button_id=7SNGNSKUQXQW2) |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

See the [**download tree**](#download-tree) for quick links to videos, landmarks, word mappings & parallel corpus.

1. [Sign Language Datasets](#sign-language-datasets)
   1. [Problem Overview](#problem-overview)
      1. [Sign Recording Options](#sign-recording-options)
      2. [Translation Dataset Needs](#translation-dataset-needs)
   2. [Datasets](#datasets)
   3. [Download Tree](#download-tree)
   4. [How to Contribute](#how-to-contribute)
   5. [Citation](#citation)
   6. [Glossary](#glossary)

Download via CLI (needs python):

```bash
pip install sign-langauge-translator
slt download "datasets/.*landmarks.*csv\.zip"
```

## Problem Overview

Sign Language is a gesture based method of communication. In sign languages, the vocabulary is small with many spoken language words corresponding to the same sign. Sentences are short and contain only the keywords. Each person has their own *accent* of performing the sign.
Every region has its own sign language and there are few large scale standardization efforts.

1. We can obtain standard dictionaries from reputable organizations in each country and concatenate signs from them using standardized grammar rules to translate & synthesize datasets.
2. We can record people performing the signs from the dictionary to capture diversity of accents.
3. We can scrape sign language videos and use deep learning to generate their glosses & translations.

Because most regional languages will have very few hours of data, the best approach will be to train a **many-to-many seq2seq translation model**.

### Sign Recording Options

Sign language can be represented as:

<details>
<summary><b>Videos</b></summary>

- Videos can consist of individual words, phrases or sentences.
- Each video can contain just one person or multiple people talking at the same time.
- Using computer vision, videos can be decomposed into 3D motion vectors of joints on the body as a preprocessing step to reduce the bias and noise in the dataset and enables more data augmentation.

</details>

<details>
<summary><b>Token Sequence + Gesture Dictionary</b></summary>

1. Sign sequence written using text word-for-word is called *gloss* and it captures the grammar of sign language.
2. There are other sign writing notations like [HamNoSys](https://en.wikipedia.org/wiki/Hamburg_Notation_System) etc which write down individual movements of the hands but this project currently only uses the word level tokens.

</details>

<details>
<summary><s>Motion capture gloves (costly for users & dataset makers)</s></summary>
</details>

### Translation Dataset Needs

<details>
<summary>A translation model requires a <i>parallel corpus</i> of sentences that should be mapped to each other.</summary>

- For each sign language video or sequence of videos, save translations & glosses in multiple languages

</details>

<details>

<summary>Sign Languages can be modeled as semi-formal languages (a mixture of rule based language & natural language). So, there is an opportunity for <b>synthetic dataset</b> generation.</summary>

- Obtain sign language [dictionaries](https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.2).
- List down all [words](https://github.com/sign-language-translator/sign-language-datasets/blob/main/dictionary/collection_to_label_to_language_to_words.json) in several text languages that can be mapped to those videos.
- Train a language model to [write sentences](https://sign-language-translator.readthedocs.io/en/latest/#complete) of only the *supported words*.
- Translate those generated sentences using [grammar rules](https://github.com/sign-language-translator/sign-language-translator/blob/main/sign_language_translator/languages/sign/sign_language.py#L62) of that regional language or a deep learning model into gloss (sign labels).
- [Concatenate videos](https://github.com/sign-language-translator/sign-language-translator/blob/main/sign_language_translator/models/text_to_sign/concatenative_synthesis.py) corresponding to the tokens in the text to synthesize parallel video.

</details>

## Datasets

The datasets currently available in the *sign_language_translator* package are chunked, preprocessed and labeled appropriately. More details on assets can be found in the release description.

<details>
<summary><b>Naming conventions</b>:</summary>

1. Dictionaries: `country-organization-number_sign-gloss.mp4`
2. Replications: `c*-o*-n*_g*_personCode_cameraAngle.mp4`
3. Sentences: `c*-o*-n*_gloss[_p*_c*].mp4`
4. Archives: `c*-o*-n*[_p*_c*].category-subcategory-extension.zip`
5. Preprocessed videos: `c*-o*-n*_g*[_p*_c*].category-embeddingModel.extension`
6. Videos without Signs: `wordless_person_camera.mp4`

- The sign labels, tokens & glosses may contain word sense disambiguation wrapped in parenthesis e.g. `*_spring(coil).mp4` or `*_spring(water-fountain).mp4`.
- Person Codes are of the format `[dh][fm]\d+`.
For example `df0001` stands for `deaf-female-0001` and `hm0002` means `hearing-male-0002`
- Camera Angles are from `(front|below|left|right|top-left|top-right)-\d+x\d+y\d+z`. (not finalized yet)
- Category in preprocessed videos and archives is from `(videos|landmarks)`.
- Subcategory in Archive name is from `mediapipe-world|mediapipe-image|mediapipe` or `dictionary(-replication)?|sentences(-replication)?`. It will include the model name in case of preprocessed files.

</details>

**Statistics**:

<table>
  <thead>
    <tr>
      <th>Sign Language</th>
      <th>Dictionary</th>
      <th>Sentences</th>
      <th>Replications</th>
      <th>Synthetic Sentences</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Pakistan</td>
      <td>
        <pre><b>Signs: 776</b> (27 min)</pre>
        <pre><b>Word Tokens</b>:<br/>en: 1591<br/>hi: 137<br/>latn-ur: 22<br/>ur: 2079</pre>
      </td>
      <td>
        <pre><b>Count: 13</b> (57 sec)</pre>
        <pre><b>Translations:</b><br/>en: 21<br/>hi: 14<br/>latn-ur: 13<br/>ur: 18</pre>
        <pre><b>Glosses</b><br/>en: 14<br/>latn-ur: 13<br/>ur: 15</pre>
      </td>
      <td>
        <b>Dictionary</b>: 22 hrs<br /><br />
        <b>Sentences</b>: 45 min
      </td>
      <td>
        <pre><b>Count: 1</b> (7 sec)</pre>
        <pre><b>Translations:</b><br/>en: 3<br/>hi: 2<br/>latn-ur: 2<br/>ur: 4</pre>
        <pre><b>Glosses</b><br/>en: 2<br/>latn-ur: 1<br/>ur: 2</pre>
      </td>
    </tr>
  </tbody>
</table>

## Download Tree

<pre>
<b style="font-size:large;">sign-language-datasets</b>
├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/README.md">README.md</a>
├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/text-preprocessing.json">text-preprocessing.json</a>
├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/todo.json">todo.json</a>
│
├── <b>asset_urls</b>
│   ├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls/archive-urls.json">archive-urls.json</a>
│   ├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls/extra-urls.json">extra-urls.json</a>
│   └── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls/pk-dictionary-urls.json">pk-dictionary-urls.json</a>
│
├── <b>parallel_texts</b>
│   ├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts/pk-dictionary-mapping.json">pk-dictionary-mapping.json</a>
│   ├── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts/pk-sentence-mapping.json">pk-sentence-mapping.json</a>
│   └── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts/pk-synthetic-sentence-mapping.json">pk-synthetic-sentence-mapping.json</a>
│
└── <b>schemas</b>
    └── <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/schemas/mapping-schema.json">mapping-schema.json</a>
</pre>

<pre>
<b style="font-size:large;">Releases</b>
├── <b><a href="https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.4">v0.0.4</a> (Landmark Datasets)</b>
│   ├── <a href="https://github.com/sign-language-translator/sign-language-datasets/releases/download/v0.0.4/pk-hfad-1.landmarks-mediapipe-world-csv.zip">pk-hfad-1.landmarks-mediapipe-world-csv.zip</a>
│   └── <a href="https://github.com/sign-language-translator/sign-language-datasets/releases/download/v0.0.4/pk-hfad-1.landmarks-mediapipe-image-csv.zip">pk-hfad-1.landmarks-mediapipe-image-csv.zip</a>
│
├── <b><a href="https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.3">v0.0.3</a> (Video Datasets)</b>
│   └── <a href="https://github.com/sign-language-translator/sign-language-datasets/releases/download/v0.0.3/pk-hfad-1.videos-mp4.zip">pk-hfad-1.videos-mp4.zip</a>
│
├── <b><a href="https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.2">v0.0.2</a> (Dictionary)</b>
│   ├── pk-hfad-1_*.mp4 [788]
│   ├── pk-hfad-2_*.mp4 [1]
│   └── wordless_wordless.mp4 [1]
│
└── <a href="https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.1"><b>v0.0.1</b></a> (Language Models for Dataset generation)
    └── *
</pre>

<!-- TODO:
pk-hfad-1_videos-dictionary-mp4.zip
pk-hfad-1_df0001_front_videos-dictionary-replication-mp4.zip

pk-hfad-2_videos-sentences-mp4.zip
pk-hfad-2_df0001_front_videos-sentences-replication-mp4.zip

pk-hfad-3_videos-dictionary-mp4.zip
pk-hfad-4_videos-sentences-mp4.zip
-->

## How to Contribute

<details>
<summary><b>Project Setup</b>:</summary>

1. Clone the repo

    ```bash
    git clone https://github.com/sign-language-translator/sign-language-datasets.git
    ```

2. [Configure JSON schema](https://code.visualstudio.com/docs/languages/json#_json-schemas-and-settings) in VSCode workspace settings especially for `*-mapping.json` files.

</details>

<details>
<summary><b>Our Needs</b>:</summary>

<details>
<summary>1. <b>Compile dictionaries</b></summary>

1. **Rename** files to follow the convention (country-organization-...)
2. **Upload** individual files to [v0.0.2 Dictionary](https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.2) release.
3. Upload zip archive to [v0.0.3 Video Datasets](https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.3) release.
4. **Link** individual file urls in [asset_urls/*-dictionary-urls.json](https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls)
5. Link archive urls into [asset_urls/archive-urls.json](https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls/archive-urls.json).
6. **Add the text tokens** that have same the meaning and can be mapped to these dictionary videos to [parallel_texts/*-dictionary-mapping.json](https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts).

</details>

<details>
<summary>2. <b>Record Dictionary Videos to capture diverse accents</b></summary>

1. **Rename** files to follow the convention (\*_personId_cameraAngle\*).
2. **Upload** zip archive to [v0.0.3 Video Datasets](https://github.com/sign-language-translator/sign-language-datasets/releases/tag/v0.0.3) release.
3. **Link** archive urls into [asset_urls/archive-urls.json](https://github.com/sign-language-translator/sign-language-datasets/blob/main/asset_urls/archive-urls.json).

</details>

<details>
<summary>3. <b>Scrape or Record sign language Sentences.</b></summary>

- Upload & Link the data
- Add translations and glosses to the [parallel corpus](https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts)

</details>

<details>
<summary>4. <b>Contribute to the <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts">Synthetic Parallel Corpus</a></b></summary>

1. Write sentences of supported words
2. Compile dataset for training a language model to do the above step.
3. Translate to other text languages

</details>

<details>
<summary>5. <b>Translate <a href="https://github.com/sign-language-translator/sign-language-datasets/blob/main/parallel_texts">existing</a> tokens, translations & glosses to other text languages.</b></summary>
</details>

</details>

> [!NOTE]\
> Ensure uniqueness in sign labels before publishing anything.

## Citation

```bibtex
@misc{mdsr2023slt_dataset,
  author       = {Mudassar Iqbal},
  title        = {Sign Language Datasets},
  year         = {2023},
  publisher    = {GitHub},
  howpublished = {\url{https://github.com/sign-language-translator/sign-language-datasets}},
  note         = {Available under the Creative Commons Attribution 4.0 International License (CC BY 4.0).}
}
```

This dataset is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You can use it for any purpose, even commercially, but you must give appropriate credit to the original creators and cite it.

## Glossary

| Word                      | Definition                                                                                                                                                                                                             |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Label                     | Text identifier of a sign language video/data sample. A filename without extension.                                                                                                                                    |
| Accent                    | A particular style of performing a sign such as speed, position and distance traveled by the hand.                                                                                                                     |
| Gloss                     | Word sequence corresponding to the signs performed in the source sign language video.                                                                                                                                  |
| Translation               | Valid text of a spoken language with the same meaning as source sign language video.                                                                                                                                   |
| Parallel Corpus           | Collection of statements in Sign Language and their translations/glosses in spoken language texts.                                                                                                                     |
| Supported Word            | A text language token (word or phrase) for which a sign language video is available in the dictionary.                                                                                                                 |
| Replication               | Videos created using the dictionary videos or web-scraped sentences as a reference clips.<br/>The performer can be hearing-abled person as well and multiple cameras from different angles can be used simultaneously. |
| Synthetic Sentence        | A sign language sentence formed by concatenating videos corresponding to word tokens written in a particular order.                                                                                                    |
| Word Sense Disambiguation | The task of figuring out the meaning or a relevant synonym of a word based on the current context.                                                                                                                     |
