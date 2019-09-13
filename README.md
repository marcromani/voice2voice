# voice2voice
Parallel data voice conversion based on [pix2pix](https://phillipi.github.io/pix2pix/).

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/marcromani/voice2voice/blob/master/LICENSE)

## Summary and contributions
It is a straightforward application of the [pix2pix](https://phillipi.github.io/pix2pix/) architecture with some minor changes.

### Data transformation
For a *(source, target)* pair of audio samples (from two different people uttering the same speech) we compute their Mel [spectograms](https://en.wikipedia.org/wiki/Spectrogram) so that each one of them is a single-channel *256x256* image. We also compute the *256x256* [DTW](https://en.wikipedia.org/wiki/Dynamic_time_warping) matrix between such samples to tackle the problem of parallel data misalignment.

### Training
During training both the source image and the distance matrix are fed to the generator as a *2x256x256* tensor, which tries to output an image that resembles the target. The distance matrix is relevant here because it provides the U-Net a way to handle non-affine temporal misalignments between source and target. In essence, the generator is conditioned twice. To our knowledge this is a novel approach. The discriminator is standard, it only sees real and fake images.

### Evaluating
Once the system is trained, to convert an audio sample from the source speaker voice to the target speaker voice, the generator is fed the source image and the zero matrix as distance matrix.

### Details
The architecture and training hyperparameters are the same as in the original paper, but we replaced the batch normalization layers by instance normalization layers both in the generator and the discriminator, as suggested in [here](https://arxiv.org/abs/1607.08022).

## Dependencies
* `librosa`
* `numpy`
* `torch`
