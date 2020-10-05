# Sloppy Butchery

Sloppy Butchery is a collection of audio processing tools for [Google Colaboratory](https://colab.research.google.com/) (i.e. your browser), using [your Google Drive](https://drive.google.com/drive/my-drive) as data source and storage.

---

# Stuttering Butcher
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyButchery/blob/main/StutteringButcher.ipynb)

Stuttering Butcher creates stutter edits and glitch on an audio file.

### Audio demos

Original audio | Stuttered | Glitched
------------ | ------------ | ------------- |
[WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-dry.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-stuttered.wav) | [WAV](https://storage.googleapis.com/olaviinha/github/stuttering-butcher/theroom1-glitch.wav) |

---

# Sloppy Noto
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/olaviinha/SloppyNoto/blob/master/sloppyNoto.ipynb)

Sloppy Noto is a data audiolizer. It interprets large sets of numeric data directly as audio signal sample magnitudes. Sloppy Noto resides in its [own repository](https://github.com/olaviinha/SloppyNoto).

### Audio Demos

Audio | Source | Description of converted data | 
------------ | ------------ | ------------- |
[WAV#1](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_xtiito_swvgej.wav) [WAV#2](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_fhurcb_yodazp.wav)| [ESA](https://esa.int) | Grating heater measurements from an ultraviolet imaging spectrograph on [Rosetta](https://en.wikipedia.org/wiki/Rosetta_(spacecraft)). |
[WAV](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_bdwqbh_smuwaa.wav)| [ESA](https://esa.int), [JAXA](https://global.jaxa.jp) | Imu Meas SC ang rate Z of AOCS Gyros and IMU on [BepiColombo](https://en.wikipedia.org/wiki/BepiColombo). |
[WAV](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_twflfr_bkezue.wav)  | [ESA](https://esa.int) | Photometric bands of flux-time pairs for given objects, bands and times measuring light curves on [Gaia](https://en.wikipedia.org/wiki/Gaia_(spacecraft)). |
[WAV](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_zzdwul_dixcmw.wav) | [NASA](https://nasa.gov) | Wave electric field intensity data from the Plasma Wave instrument on [Voyager 2](https://en.wikipedia.org/wiki/Voyager_2) from the Jupiter encounter. |
[WAV](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_lijild_fyvgno.wav)| [HSY](https://hsy.fi) | Air quality from Aeromon BH-12 on [moving trams](https://en.wikipedia.org/wiki/Helsinki_tram_network) in Helsinki. |
[WAV](https://storage.googleapis.com/olaviinha/github/sloppy-noto/noto_wclazy_febwrp.wav)| [FVH](https://forumvirium.fi/) | Water temperatures of several swim beaches in Helsinki. |

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
