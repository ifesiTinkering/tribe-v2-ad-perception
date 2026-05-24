# tribe-v2-ad-perception

**Can a brain encoding model find the emotional climax of an ad it has never seen?**

This repository contains the experiment notebook behind [*Your AI Focus Group Can't Hear the Music*](https://medium.com/@ifesionubogu/your-ai-focus-group-cant-hear-the-music-211964cd7460), a comparison of Meta's [TRIBE v2](https://github.com/facebookresearch/tribev2) brain encoding model against an LLM (Claude Sonnet) at identifying documented peak emotional moments in iconic video ads.

## What this is

TRIBE v2 takes in video, audio, and text and predicts second-by-second cortical activation across ~20,000 points on the brain surface. It was trained on fMRI data from 720+ people watching movies and listening to stories. It has never seen a commercial.

I fed it three ads with well-documented emotional climaxes (sourced from directors, neuroscience studies, and press coverage before running any experiments), then checked whether its predicted brain activation peaks landed on those moments. I ran the same ads through Claude Sonnet (100 independent trials per ad, temperature 1.0, still frames only) as a comparison.

## Key findings

**LLMs analyzing video from still frames are analyzing muted television.** The core result across three experiments:

- **When the peak is visual (Apple 1984, hammer throw/screen explosion):** Both systems converge on the same second. 98% LLM consensus. No gap.
- **When the peak is audio-driven (Cadbury Gorilla, Phil Collins drum fill):** The brain model finds the audio onset of the drum fill at second 59. The LLM, working from frames, lands on second 63, the frame where drumming is visually obvious. A 4-second gap that maps directly to the difference between hearing drums start and seeing a gorilla mid-swing.
- **When the peak is a narrative beat tied to an audio transition (AirPods "Quiet the Noise," crash-down at second 35):** Neither system puts it as #1. Both are drawn to moments of higher raw visual complexity. The moments people remember and write about are not always the moments of maximum perceptual intensity. Perception and meaning are different things.

## Concrete lessons from the experiments

1. **Models are only as good as the modalities they can process.** An LLM working from extracted frames has no access to audio. For the Cadbury Gorilla, the entire emotional architecture of the ad is built by 60 seconds of Phil Collins. Mute it and you are watching a gorilla sit still then move its arms. No amount of visual analysis recovers what makes that ad work. This is not a subtle limitation; it is a structural one.

2. **Training data recognition is not the same as perception.** Claude recognized all three ads 100/100. It "knows" the Gorilla drum fill is the peak because it has seen people write about it. But even with that knowledge, it is anchored to the visually obvious frame, not the audio onset. Recognition gets you to the right neighborhood. Perception gets you to the right second.

3. **Perceptual intensity and memorability are not the same thing.** The AirPods experiment showed this clearly. The brain model's top peaks and the LLM's top picks both landed on moments of maximum visual spectacle, not on the crash-down at second 35 that generated all the press coverage. The moment that sticks with people is a narrative beat, not a sensory peak. Brain activation measures what the cortex is doing. It does not measure what the viewer will remember tomorrow.

4. **Out-of-distribution generalization is the real test.** TRIBE v2 was trained on Friends episodes and feature films, zero commercials. Finding the Gorilla drum fill within one second and the 1984 hammer throw at the exact documented window, on content it was never trained on, is a meaningful signal that the model is capturing something general about perceptual processing rather than memorizing training data.

## Current perspective

This experiment was a useful way to build empirical intuition about where current models break down. My research focus has since shifted toward AI safety, interpretability, and scalable oversight. The throughline is the same: understanding what models actually do versus what we assume they do. The audio perception gap in this experiment is a concrete, measurable instance of a broader pattern where model capabilities are bounded by their input modalities and training objectives in ways that are easy to miss if you only evaluate on cases where the answer happens to be visually obvious.

## Repository contents

- `tribe_v2_ad_perception.ipynb` — Full experiment notebook (runs on Google Colab with A100 GPU)
  - TRIBE v2 brain activation timelines for all three ads
  - 100-trial LLM comparison per ad (Claude Sonnet, temperature 1.0)
  - Visualizations and statistical summaries

## How to run

Runs on Google Colab with an A100 GPU. Requirements:
- TRIBE v2 (`pip install` from [Meta's GitHub](https://github.com/facebookresearch/tribev2))
- Anthropic API key (for the LLM comparison trials)
- HuggingFace account with LLaMA 3.2 access

## Read more

For the full writeup with sourced ground truth documentation, director interviews, neuroscience studies, and detailed analysis of each experiment: [*Your AI Focus Group Can't Hear the Music*](https://medium.com/@ifesionubogu/your-ai-focus-group-cant-hear-the-music-211964cd7460)

## Author

[Ifesi Onubogu](https://www.linkedin.com/in/ifesionubogu) · [ifesionubogu@gmail.com](mailto:ifesionubogu@gmail.com)
