# Sloppy Butchery

Sloppy Butchery is a collection of different slicing based audio processing tools for [Google Colaboratory](https://colab.research.google.com/) (i.e. your browser), using [your Google Drive](https://drive.google.com/drive/my-drive) as data source and storage.

---

# Sloppy Butcher
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

# Stuttering Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/StutteringButcher.ipynb)

Stuttering Butcher creates stutter edits and glitch on an audio file.

### Audio demos

Original audio | Stuttered | Glitched
------------ | ------------ | ------------- |
[WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-dry.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-stuttered.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-glitch.wav) |

---

# Poetic Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/PoeticButcher.ipynb)

Poetic butcher is a speech-to-words slicer. It slices speech audio to individual words using [Mozilla Deepspeech](https://github.com/mozilla/DeepSpeech) 
recurrent neural network.

---

# Senior Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/SeniorButcher.ipynb)

Senior Butcher is a beat-slicer that improves the beat tracking precision of audio analysis libraries such as Librosa, Essentia or Aubio, particularly for the purpose of beat slicing.

### Audio demos

Track | Librosa | Butcher, _ours_
------------ | ------------ | ------------- |
Aphex Twin - Windowlicker | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_windowlicker.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_windowlicker.mp3)  |
Boards of Canada - Peacock Tail | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_boc-peacocktail.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_boc-peacocktail.mp3)  |
2Unlimited - No Limit | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_librosa_2unlimited-nolimit.mp3) | [MP3](https://storage.googleapis.com/olaviinha/hpbs/demo_pbs_2unlimited-nolimit.mp3)

### Methodology for precision improvement

1. **Drum track extraction for timing:** Stem track of drums is extracted from input audio by [Deezer Spleeter](https://github.com/deezer/spleeter) convolutional neural network to be used as a _timing track_. Timing track is used for initial estimation of beat positions, i.e. input audio track (audiofile#1) is eventually sliced according to analysis performed on the timing track (audiofile#2).

2. **Duration refinements by lossy compression of beat interval distribution:** After initial beat tracking is performed according to timing track, beat durations are calculated from beat position distribution. Significant duration range is constricted by finding the modal value of approximated beat intervals. Currently the minimum beat duration within the significant range is eventually used as new absolute beat duration, which may increase the track tempo by a fraction of a bpm. This is likely to be optimized in the future.

3. **Tail peak cluster shaving:** Marginally prolonged beat duration outside the significant range is used for detection of high concentrations of peaks at the tail. These peak clusters are assumed subsequent beat beginnings. Should such peak cluster occur, beat start position is nudged backwards in time until the cluster at hand is positioned in the subsequent slice of a beat. 

---

## Other utilities

- [util_AudioConcat.ipynb](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/util_AudioConcat.ipynb) concatenates a directory of audio files into one or more WAV files.
- [util_librosa_functions.ipynb](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/util_librosa_functions.ipynb) is a tiny collection (or cheatsheet) of various audio processing related functions from all of these notebooks in one place. Functions are built mainly around Librosa and Numpy, and perhaps useful to some for development purposes; no need to re-invent things like _fade out_.
- [sloppyNoto.ipynb](https://colab.research.google.com/github/olaviinha/SloppyNoto/blob/master/sloppyNoto.ipynb) is a data audiolizer residing in it's [own repository](https://github.com/olaviinha/SloppyNoto). It turns numeric data into audio by interpreting it as digital audio signal sample magnitudes.

---

**DO NOT DONATE.** It is illegal for a Finnish citizen to plea for donations, and a donate button placed in the interwebs is interpreted as such plea by the Finnish authorities. Please DO NOT send any donations to [my Paypal](https://paypal.me/oinha) to cover any development related expenses, **especially** if you find these tools useful and want to show support. Use [this Paypal link](https://paypal.me/oinha) for anything but donations. **DO NOT DONATE.**
