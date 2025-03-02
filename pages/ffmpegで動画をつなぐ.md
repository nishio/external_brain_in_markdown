
OsmoActionで長時間の動画を撮ると4ギガごとに分割される
これをつなぐためだけにPremiereを使うのも面倒なので[[ffmpeg]]でやる

対象ファイルの名前を各行に、行頭に`file `をつけて書いたファイルを用意する
`$ ls DJI_0577* | sed -e 's/^/file /' > t.txt`

結合する
`$ ffmpeg -f concat -i t.txt -c copy output.mp4`
出力：`frame=184209 fps=491 q=-1.0 Lsize=75104689kB time=01:42:26.40 bitrate=100100.4kbits/s speed=16.4x`

でもまあ単に結合しただけなので77ギガのファイルができちゃう
`-rwxr-xr-x 1 nishio nishio 76907201729  1月 20 15:13 output.mp4`

[Encode/YouTube – FFmpeg](https://trac.ffmpeg.org/wiki/Encode/YouTube)
`$ ffmpeg -i input.avi -c:v libx264 -preset slow -crf 18 -c:a copy -pix_fmt yuv420p output.mkv`
[[.mkv]]とは[Matroska - Wikipedia](https://ja.wikipedia.org/wiki/Matroska)

`-rwxr-xr-x 1 nishio nishio  2573372618  1月 20 19:07 output.mkv`
`-rwxr-xr-x 1 nishio nishio 76907201729  1月 20 15:13 output.mp4`

mkvはPremiereで開けない…
そのままYouTubeにアップロードしてみる
![image](https://gyazo.com/8a08d3b1e302acb16e0476957c1d3b80/thumb/1000)
6:44???

