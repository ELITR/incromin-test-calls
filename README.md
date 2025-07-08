# InCroMin

This data package contains published parts of InCroMin, a corpus of
cross-lingual dialogues with minutes and detection of misunderstandings. 

InCroMin is described in a paper **Corpus of Cross-lingual Dialogues with Minutes
and Detection of Misunderstandings,** by Marko Čechovič, Natália Komorníková,
Dominik Macháček, and Ondřej Bojar. To be published in TSD 2025.

The data were created by volunteering participants, by 2-5 people in each
meeting. They were matched in a way that there are at least two groups of
people who did not understand each other's language. Their meeting was facilitated by
simultaneous speech translation tool integrated in Minuteman. The meetings were
held via a teleconferencing platform that recorded each speaker in a separate
audio track. The participants gave consent with data processing and release.

Then, their speech was automatically transcribed in their original language, and
automatically translated into English.  Then, human annotators manually corrected
transcripts and translations, and deidentified audio and texts by removing
confidential information such as person names. The annotators also created minutes.

InCroMin corpus is a very useful data set intended primarily for evaluating
automatic systems that aim to facilitate cross-lingual dialogues in realistic
conditions and end-to-end.  It can evaluate Automatic Speech Processing, Speech
Translation, Simultaneous Speech Translation, Quality Estimation, and Automatic
Minuting.

## Filename conventions

The data are located in the directory `meetings/` in subdirectories mentioning the language combination used in the meeting. 
For instance, ``hu_uk_1`` is the first call between a speaker speaking Hungarian (language code `hu` language) and a speaker speaking Ukrainian (language code `uk`), while `cs_cs_zh_1` is a call between two Czech speakers (`cs`) and one Chinese speaker (`zh`). The language codes are sorted alphabetically.

Within each subdirectory, there are filenames associated to each speaker. The
speakers are identified with an initial enumerating the alphabet (A, B, C, ...).
The same speaker can appear in multiple meetings but for higher privacy, there is no linking of speakers across the meetings.

For each speaker, the following filenames and filename suffixes are used:

| Filename / suffix | Explanation | When missing  |
| -------- | ----------- | ------------- |
| `[A-E]`                    | enumerated initial of the speaker  | - |
| `pt` / `pt-BR` | speaker's primary language or language-country code | - |
| `A_pt.mp3`                 | speaker's deidentified audio                                      | speaker does not consent, or deidentification pending       | 
| `.tt.txt`                 | timestamped text (see below) | `.txt` without `.tt` means that the timestamps are pending |
| `A_pt_audiodeident.tt.txt` | time segments of the audio that were deidentified (replaced with silence) | audio deidentification was not needed |
| `A_ru-B-zh.mp3` | rarely, two speakers are recorded in one audio track |     |
| `*_diarization*.tt.txt` | rarerly, diarization indicates in what time segments spoke who | not needed for one channel per speaker, or it's pending |
| `A_pt.tt.txt`    | deidentified ASR transcript | it's pending. No ASR was used in manual correction |
| `A_en.tt.txt` | deidentified automatic translation by some system / by Whisper into English | it's pending. No automatic translation was used in manual correction. |
| `*_corrected.tt.txt` | deidentified manually corrected transcript or translation (or, rarely, diarization) | it's pending |

Moreover, the meeting directories also contain a file `minutes.txt` containing the minutes (written summaries) in English.

Note that some files can be missing, due to pending deidentification check, lack of resources for manual annotation, insufficient consents from the original speakers or accidental data loss.

### Timestamped text = `.tt.txt` format description

- 3 tab-delimited columns: 
	- columns 1-2: begining and end time of the segment, as decimal number in seconds from the beginning of audio
	- column 3: text

- this format matches Audacity label track format, so these files can be opened and inspected in Audacity along
  the corresponding audio track

Example: 

```
34.0500 54.9420 Do you hear me now? Yeah, but I don't speak Czech.
134.1460  162.750 My project was already in the process of completion.
```

- audiodeident and diarization follow the same format, except a simple text or speaker id and language in column 3

#### Deidentification

Deidentified terms in texts are replaced with placeholders wrapped in underscores, such us `__PERSON1__` . The terms are consistent within the same meetings.

The types of entities are inspired by the [ELITR minuting corpus](https://ufal.mff.cuni.cz/elitr-minuting-corpus). 

### Transcripts and translations

Typically, each speaker has attached following text files:

| Filename | Explanation |
| -------- | ----------- |
| `A_hy.tt.txt` | fully automatic ASR output, with automatic segment-level timestamps |
| `A_hy_corrected.tt.txt` | manually revised correction of ASR. Timestamps remain unrevised, automatic only. |  
| `A_en.tt.txt` | fully automatic translation into English, with automatic segment-level timestamps |
| `A_en_corrected.tt.txt` | manually revised correction of automatic translation. Timestamps remain unrevised, automatic only. |

#### Automatic systems

- the automatic systems that were used are documented in the metadata
- the systems are:
 - Whisper large-v3, used either for ASR in the original language, without automatic language ID, and with VAD, or for translation from speech directly into English
 - Deepl -- text translation from the best available transcript into English
 - some 
- `ru_zh_2/A_ru-B_zh.diarization_corrected.tt.txt` was created with Pyannote and then manually corrected in a way that 
the silence between speakers is attached to the closer speaker.



## Metadata

- `README.md` -- this file

- `metadata.ods` is a spreadsheet containing:

  - summary of what data items are available, reasons for unavailability, if other than annotation pending
  - the automatic system that were used to create each transcript or translation
  - or information which corrected translations/transcriptions were created without any automated system

## Releases

### Pre-release versions

Pre-release versions are in https://github.com/ELITR/incromin-test-calls .
The authors welcome contributions such as language corrections or adding new or missing annotations.  

The released versions are tagged in GitHub and also submitted to the persistent repository Lindat.

### InCroMin 1.0

It is the *first release* mentioned in the TSD paper, plus 4 additional meetings.
Released in July 2025.
