# Sloppy Butchery

Sloppy Butchery is a collection of [Colab notebooks](https://colab.research.google.com/) for various audio processing tools.

---

## Sloppy Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/SloppyButcher.ipynb)

Sloppy Butcher is an audio power-chopper and randomizer. It takes a directory of audio files, chops it, shuffles it, and frankensteins it up into a single audio file according to your BPM, effects and other settings.

### Audio demos

Source description | Result
------------ | ------------
Random full length african choir-like songs. | [MP3](https://olaviinha.storage.googleapis.com/sloppyButcher-randomafricansongs.mp3)
Random clips of Neurofunk tracks. | [WAV](https://storage.googleapis.com/olaviinha/github/sloppy-butcher/frankenstein_qaxu_20201018-195708__162bpm.wav)
Random full length songs. | [MP3](https://olaviinha.storage.googleapis.com/sloppyButcher-deeperhellpreset.mp3)
Random full length finnish pop songs. | [MP3](https://olaviinha.storage.googleapis.com/sloppyButcher-randomfinnishsongs.mp3)

---

## Autotune
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/Autotune.ipynb)

Autotune autotunes audio file to a) nearest note, b) a scale, c) another audio file or d) [Chords Guru Turbo 100a Deluxe](https://ki.gy/cv) chord progression.

### Audio demos

Source description | Result
------------ | ------------
Original | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-dry.wav)
Autotuned flat C | [WAV](https://storage.googleapis.com/olaviinha/github/sloppy-butchery/theroom1-cmaj.wav)
Autotuned to [1994 Nokia Tune](https://www.youtube.com/watch?v=Vk4KK-gh0FM) | [WAV](https://storage.googleapis.com/olaviinha/github/sloppy-butchery/theroom1-nokiatune.wav)
Autotuned to a chord progression | [WAV](https://storage.googleapis.com/olaviinha/github/sloppy-butchery/theroom1-chordprog.wav)


---

## Stuttering Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/StutteringButcher.ipynb)

Stuttering Butcher applies stutter edits and glitch on an audio file according to settings.

### Audio demos

Original audio | Stuttered | Glitched
------------ | ------------ | ------------- |
[WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-dry.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-stuttered.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-glitch.wav) |

---

## Poetic Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/PoeticButcher.ipynb)

Poetic butcher is a voice isolator and speech-to-words slicer. It isolates voice from audio source using [Deezer Spleeter](https://github.com/deezer/spleeter) (convolutional neural network) and/or slices it to individual words according to settings using [Mozilla Deepspeech](https://github.com/mozilla/DeepSpeech) (recurrent neural network).

---

## Senior Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/SeniorButcher.ipynb)

Senior Butcher is a beat-slicer that improves the beat tracking precision of audio analysis libraries such as Librosa, Essentia or Aubio, particularly for the purpose of beat slicing.

### Audio demos

Track | Librosa | Butcher, _ours_
------------ | ------------ | ------------- |
Aphex Twin - Windowlicker | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_windowlicker.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_windowlicker.mp3)  |
Boards of Canada - Peacock Tail | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_boc-peacocktail.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_boc-peacocktail.mp3)  |
2Unlimited - No Limit | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_2unlimited-nolimit.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_2unlimited-nolimit.mp3)

### Methodology for precision improvement

1. **Drum track extraction for timing:** Stem track of drums is extracted from input audio by [Deezer Spleeter](https://github.com/deezer/spleeter) (convolutional neural network) to be used as a _timing track_. Timing track is used for initial estimation of beat positions, i.e. input audio track (audiofile#1) is eventually sliced according to analysis performed on the timing track (audiofile#2).

2. **Duration refinements by lossy compression of beat interval distribution:** After initial beat tracking is performed according to timing track, beat durations are calculated from beat position distribution. Significant duration range is constricted by finding the modal value of approximated beat intervals. Currently the minimum beat duration within the significant range is eventually used as new absolute beat duration, which may increase the track tempo by a fraction of a bpm. This is likely to be optimized in the future.

3. **Tail peak cluster shaving:** Marginally prolonged beat duration outside the significant range is used for detection of high concentrations of peaks at the tail. These peak clusters are assumed subsequent beat beginnings. Should such peak cluster occur, beat start position is nudged backwards in time until the cluster at hand is positioned in the subsequent slice of a beat. 

---

## Audio Concat
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/util_AudioConcat.ipynb)

Audio Concat takes a directory of audio files and glues them together into one or more WAV files. This notebook was originally created to concatenate thousands of very short audio files produced by neural networks, and basically this notebook sparked the idea to create all the other notebooks in this repository.

---

## Other notebooks

- [util_librosa_functions.ipynb](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/util_librosa_functions.ipynb) is a cheatsheet of NumPy/librosa based audio-processing functions from all of these notebooks in one place. The aim is to keep these functions independent, but this is unlikely the case due to lack of time. Nevertheless, it may provide some aid for audio processing in Python.

## You may also be interested in...
- [sloppyNoto.ipynb](https://colab.research.google.com/github/olaviinha/SloppyNoto/blob/master/sloppyNoto.ipynb) is a data audiolizer residing in it's [own repository](https://github.com/olaviinha/SloppyNoto). It turns numeric data into audio by interpreting it as digital audio signal sample magnitudes.
