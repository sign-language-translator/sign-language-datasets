# sign-language-datasets
Datasets for sign language translation.

- Pakistani Sign Language Clips: 840 clips performed by 12 people (10 normies, 2 hearing impaired).
    - Labeled in Urdu & English.
- Text2Text: Spoken Language Text to Sign Language Text (restructure & shorten) (both Urdu & English).
- English & Urdu Text Corpora used in synthethetic data generation (contain all and only the supported words).

# Definitions
- gloss: word sequence corresponding to sign sequence for a given complete spoken language text.

# Explanations
- json ...

# Directory Tree
    sign-language-datasets
    ├── sign_recordings
    │   ├── features
    │   │   └── landmarks
    │   │
    │   ├── reference_clips
    │   │   ├── pk-hfad-1 [788]
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

# Bonus
##### new file size command
    git status -u --porcelain | awk '{print $2}' | xargs ls -hl | awk '{print $5 "\t" $9}'