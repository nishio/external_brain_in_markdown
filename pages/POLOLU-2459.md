
[[フォトリフレクタ]]
デジタル出力が出るのでADCがないRasPiでも読めるが、GPIOの電圧でON/OFFを見るのではなく、outputにしてHIを出力した後、readしつづけてLOに戻るまでの時間を測るって使い方をする

- Set the I/O line to an output and drive it high.
- Allow at least 10 μs for the sensor output to rise.
- Make the I/O line an input (high impedance).
- Measure the time for the voltage to decay by waiting for the I/O line to go low.
[Pololu - QTR-1RC Reflectance Sensor (2-Pack)](https://www.pololu.com/product/2459)

- メーカーの出してるライブラリとセットでArduinoで使うなら良いかもしれない
- 「デジタル出力だからADCのないRasPiでも使えるぞ！」とか思ったけど、めんどくさい

いちおう使えてはいる [ソースコード](https://gist.github.com/nishio/8dd862a127b0d8045d23aac90c9c9b27)
