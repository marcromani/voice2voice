# voice2voice
Parallel data voice conversion based on the [pix2pix](https://phillipi.github.io/pix2pix/) architecture.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/marcromani/voice2voice/blob/master/LICENSE)

## Summary
Non-conditional GAN system (neither the generator nor the discriminator are conditioned) based on the [pix2pix](https://phillipi.github.io/pix2pix/) architecture. The aim is to reconstruct the speech of a source speaker with the voice of a target speaker. The models are not conditioned because it is not possible to learn a meaningful mapping given the (non-linear) audio misalignments due to, for example, source and target speakers speaking at different speeds.

## Data
We trained and tested the system with the [Voice Conversion Challenge 2018](https://datashare.is.ed.ac.uk/handle/10283/3061) data. For a *(source, target)* pair of audio samples (from two different people uttering the same speech) we compute their Mel [spectograms](https://en.wikipedia.org/wiki/Spectrogram) so that each one of them is a single-channel *256x256* image. These are the inputs of both the generator and the discriminator.

![](https://github.com/marcromani/voice2voice/blob/master/outputs/source_5.png "source") | ![](https://github.com/marcromani/voice2voice/blob/master/outputs/target_5.png "target")
:-:|:-:
Source | Target

## Details
The architecture and training hyperparameters are the same as in the original paper, but we replaced the batch normalization layers by instance normalization layers both in the generator and the discriminator, as suggested [here](https://arxiv.org/abs/1607.08022). Also, we use mean squared error as the adversarial loss, as suggested [here](https://arxiv.org/abs/1611.04076).

## Dependencies
* [`librosa`](https://librosa.github.io/librosa/index.html#)
* [`numpy`](https://numpy.org/)
* [`torch`](https://pytorch.org/)

## Examples
[![](https://github.com/marcromani/voice2voice/blob/master/outputs/source_1.png "source")](https://github.com/marcromani/voice2voice/blob/master/outputs/source_1.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/target_1.png "target")](https://github.com/marcromani/voice2voice/blob/master/outputs/target_1.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_1.png "fake")](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_1.wav)
:-:|:-:|:-:
Source | Target | Fake

[![](https://github.com/marcromani/voice2voice/blob/master/outputs/source_2.png "source")](https://github.com/marcromani/voice2voice/blob/master/outputs/source_2.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/target_2.png "target")](https://github.com/marcromani/voice2voice/blob/master/outputs/target_2.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_2.png "fake")](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_2.wav)
:-:|:-:|:-:
Source | Target | Fake

[![](https://github.com/marcromani/voice2voice/blob/master/outputs/source_3.png "source")](https://github.com/marcromani/voice2voice/blob/master/outputs/source_3.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/target_3.png "target")](https://github.com/marcromani/voice2voice/blob/master/outputs/target_3.wav) | [![](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_3.png "fake")](https://github.com/marcromani/voice2voice/blob/master/outputs/fake_3.wav)
:-:|:-:|:-:
Source | Target | Fake
