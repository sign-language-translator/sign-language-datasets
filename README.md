# sign-language-datasets

Datasets for sign language translation. [See release files for big data files](https://github.com/sign-language-translator/sign-language-datasets/releases)

This project includes:

- Reference Clips
  - pakistan-hamza_foundation (pk-hfad) [788+1]
  - wordless (~10 minutes of a person doing everything except signs)
- Word Mapping (which spoken language words map to which sign language clips or sequence of clips)
- Videos (Recordings)
  - 12 people performing pk-hfad and wordless in 4 camera angles (front, left, right, below)
  - Male : Female = 1 : 1
  - The left and right camera angles are half of the times top-left or top-right
- Text Corpora
  - A parallel corpus of spoken language sentences and their corresponding sign language gloss (clip sequence)

## Definitions

- gloss: word sequence corresponding to sign sequence for a given complete spoken language text.

## Explanations

- json ...

## Directory Tree

```text
    sign-language-datasets
    ├── sign_recordings
    │   ├── features
    │   │   └── landmarks
    │   │
    │   ├── reference_clips
    │   │   ├── pk-hfad-1 [788]
    │   │   ├── pk-hfad-2 [1]
    │   │   └── wordless [1]
    │   │
    │   └── videos
    │       ├── pk-hfad-1
    │       │   ├── person101 [3152]
    │       │   ├── person151
    │       │   ├── person201
    │       │   ├── person202
    │       │   ├── person203
    │       │   ├── person204
    │       │   ├── person205
    │       │   ├── person251 [3147]
    │       │   ├── person252 [3151]
    │       │   ├── person253 [3152]
    │       │   ├── person254
    │       │   └── person255
    │       │
    │       └── wordless
    │           ├── person101 [4]
    │           ├── person151
    │           ├── person201
    │           ├── person202
    │           ├── person203
    │           ├── person204
    │           ├── person205
    │           ├── person251
    │           ├── person252
    │           ├── person253
    │           ├── person254
    │           └── person255
    │
    └── text_corpora
        ├── parallel_corpus.json
        ├── supported_substrings_frequency.json
        └── raw_corpora
            └── wikipedia.json
```

## Bonus

**new file size command**

```bash
git status -u --porcelain | awk '{print $2}' | xargs ls -hl | awk '{print $5 "\t" $9}'
```
