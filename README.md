# incromin-test-calls
This repository contains published parts test cross-lingual calls, collected and annotated as part of the InCroMin project (an FSTP under the EU project UTTER).


## Filename Conventions

The data are located in directories mentioning the language combination used in the call. For instance ``uk_hu`` is a call between a speaker speaking Ukrainian and a speaker speaking Hungarian while ``pt-BR_cs`` is a call between a speaker of Brazillian Portuguese and a Czech speaker.

There are at least two speakers in each call directory. We also have a call between four speakers.

The order of the languages in the directory name is preferably chosen to reflect the volume spoken in the language with the more used languages coming first.

Within each directory, the following filenames and filename suffixes are used.

Note that some files can be missing, due to pending deidentification check, lack of resources for manual annotation, insufficient consents from the original speakers or accidental data loss.

The speakers are identified using an initial. No two speakers of in the same call have the same initial. The same initial accross different calls does not mean the same speaker, of course.

In the example below, we use speaker A speaking primarily Armenian (language code ``hy``) and B speaking primarily Czech (``cs``). Occasionally speakers use English, too, but that should only be an exception.


**Audio files**
```
A_hy.mp3            ... the sound of speaker A in mp3; with silence when speaker
                        B was speaking
B_cs.mp3            ... the corresponding sound of speaker B
A_hy-B_cs.mp3       ... rarely, the channels were joint into one track
```

**Timestamped txt files**

Transcripts and translations are timestamped (except a few cases where the timestamps could not be recovered easily) and follow this convention:

- 3 tab-delimited columns: 
	- columns 1-2: begining and end time of the segment, as decimal number in seconds
	- column 3: text
- this format matches Audacity label track format, so these files can be opened and inspected in Audacity along
  the corresponding audio track
- whenever a file contains timestamps in this format, its name must end with ``.tt.txt``

The corpus contains these types of timestamped files:

```
A_hy_whisperASR.tt.txt ... fully automatic timestamped output of Whisper ASR
                           (in some directories, this is still called A_hy.txt)
A_hy_whisperASR_corrected.tt.txt ... it's A_hy_whisperASR.tt.txt file that is
                                     manually corrected 
A_en_whisperST.tt.txt  ... fully automatic timestamped output of Whisper direct
                           sound translation from the original language to English
                           (in some directories, this is still called A_en.txt)
A_en_whisperST_corrected.tt.txt ... it's A_en_whisperST.tt.txt file that is
                                    manually corrected 
```


**Non-timestamped txt files**

When the timestamps are not available or not relevant, the filenames end with just ``.txt``, not ``.tt.txt``.

We have these non-timestamped files:

```
A_has_seen_hy.txt   ... the live transcript that was shown to A in Armenian
```
