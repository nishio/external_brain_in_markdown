---
title: "Whisper"
---

2022-12-19
`$ pip install git+https://github.com/openai/whisper.git`
`$ ffmpeg -ss 00:00:00 -to 00:10:00 -i ~/Downloads/KJ法勉強会振り返り勉強会.mp4 -c copy tmp.mp4`
`$ whisper tmp.mp4 --language Japanese --model large`
- `UserWarning: FP16 is not supported on CPU; using FP32 instead`
- `whisper tmp.mp4 --language Japanese --model large  617.96s user 340.21s system 188% cpu 8:28.80 total`
- `--device mps`

- `[01:03:27.660 --> 01:03:55.660] ご清聴ありがとうございました`
    - whisper tmp.mp4 --language Japanese --model large  38903.09s user 20685.49s system 150% cpu 11:01:14.63 total

2023-04-30
[https://fukugyouhistory.tokyo/?p=1207](https://fukugyouhistory.tokyo/?p=1207)
[GitHub - guillaumekln/faster-whisper: Faster Whisper transcription with CTranslate2](https://github.com/guillaumekln/faster-whisper)


[[yt-dlp]]
- [GitHub - yt-dlp/yt-dlp: A youtube-dl fork with additional features and fixes](https://github.com/yt-dlp/yt-dlp)

