
Ergodox EZに関する情報を未来の自分のためにまとめる。

- これは何？
    - 回路図とファームウェアが公開されているキーボード
    - [Teensy USB Development Board](https://www.pjrc.com/teensy/)
    - Atmega32U4
    - 右手と左手が別れていて、間の通信はI2C
        - 物理的には4極ステレオケーブルで接続されている
        - 先端を1として、4がGND。回路図的には1からSCL, SDA, VCCだと思うのだけど未検証
        - VCCは5V
    - I2Cエキスパンダが両側についている

ソース
- [https://github.com/jackhumbert/qmk_firmware/tree/master/keyboards/ergodox](https://github.com/jackhumbert/qmk_firmware/tree/master/keyboards/ergodox)

ビルドガイド [https://github.com/qmk/qmk_firmware/blob/master/docs/BUILD_GUIDE.md](https://github.com/qmk/qmk_firmware/blob/master/docs/BUILD_GUIDE.md)
:

```
$ cd /home/nishio/ergodox/qmk_firmware/keyboards/ergodox
$ make nishio
```


!2C関連
    - keyboards/ergodox/ez/i2cmaster.h
    - keyboards/ergodox/ez/twimaster.c

回路図
- [https://github.com/ErgoDox-EZ/docs/](https://github.com/ErgoDox-EZ/docs/)
    - 僕が買ったErgodox EZの基板は2260
        - 中を開けて確認した
            - 中を開けるときは裏のシールを剥がす

ファーム読解
- keyboard_task
    - [https://github.com/qmk/qmk_firmware/blob/master/tmk_core/common/keyboard.c#L154](https://github.com/qmk/qmk_firmware/blob/master/tmk_core/common/keyboard.c#L154)
c

```c
/*
 * Do keyboard routine jobs: scan mantrix, light LEDs, ...
 * This is repeatedly called as fast as possible.
 */
void keyboard_task(void)
{...
```

    - 中で`matrix_scan();`を呼びまくっている
- matrix_scan
    - [https://github.com/qmk/qmk_firmware/blob/master/keyboards/ergodox/ez/matrix.c#L174](https://github.com/qmk/qmk_firmware/blob/master/keyboards/ergodox/ez/matrix.c#L174)
    - 左側のキーボードがつながってるかどうか接続を挑戦してみてる
c

```c
uint8_t matrix_scan(void)
{
    if (mcp23018_status) { // if there was an error
        if (++mcp23018_reset_loop == 0) {
            // since mcp23018_reset_loop is 8 bit - we'll try to reset once in 255 matrix scans
            // this will be approx bit more frequent than once per second
            print("trying to reset mcp23018\n");
            mcp23018_status = init_mcp23018();
            if (mcp23018_status) {
                print("left side not responding\n");
            } else {
                print("left side attached\n");
                ergodox_blink_all_leds();
            }
        }
    }
```

- init_mcp23018
    - [https://github.com/qmk/qmk_firmware/blob/master/keyboards/ergodox/ez/ez.c#L50](https://github.com/qmk/qmk_firmware/blob/master/keyboards/ergodox/ez/ez.c#L50)

- deleyのやりかた
c

```c
_delay_ms(50);
```


- デバッグコンソール
    - [https://github.com/tmk/tmk_keyboard/wiki/FAQ#debug-console](https://github.com/tmk/tmk_keyboard/wiki/FAQ#debug-console)
    - CDC
        - [http://www.recursion.jp/prose/avrcdc/driverj.html](http://www.recursion.jp/prose/avrcdc/driverj.html)
        - USBの上でR232Cが走る
    - デバッグコンソール
        - [https://www.pjrc.com/teensy/hid_listen.html](https://www.pjrc.com/teensy/hid_listen.html)
    - デバイスが見つからない
        - ソース読んだらhid = rawhid_open_only1(0, 0, 0xFF31, 0x0074);してreadしてる
            - これの実装はここにある
                - [https://github.com/raphendyr/teensy-listen/blob/master/rawhid.c#L71](https://github.com/raphendyr/teensy-listen/blob/master/rawhid.c#L71)

- LEDデバッグ
    - ergodox_right_led_1_on();
    - ergodox_led_all_off();
    - ergodox_led_all_set(LED_BRIGHTNESS_HI);


- 右側のみ、通常接続では1が半分つく
    - ケーブルを抜くと1が消える
        - その後さしても戻らない
- 右側のみで起動して、ブレッドボードをさすと1が消える
c

```c
void init_7seg(void)
{
  ergodox_led_all_off();
  ergodox_led_all_set(LED_BRIGHTNESS_HI);
  i2c_init();
  ergodox_right_led_2_on();
  i2c_start(0x70);
  ergodox_right_led_3_on();

  i2c_write(0x21);
  i2c_stop();
  _delay_ms(10);

  i2c_start(0x70);
  i2c_write(0x81);
  i2c_stop();
  _delay_ms(10);

  i2c_start(0x70);
  i2c_write(0xEF);
  i2c_stop();
  _delay_ms(10);
  ergodox_right_led_1_on();
}

```


- TRRS
    - グランドは正しそう
    - 枝付きバスは4つが4つに正しく導通していることを確認済み
        - TRRS順で緑黒緑黒、1と2にシールを貼って置いた
    - VCCとGNDだけLEDにつないだ状態でI2Cバスとして機能しなくなる
    - GNDは正しそう
        - VCCを3に指すとバスが機能しなくなる
        - 抜くと戻る
        - 2に指すと機能しなくなり、抜いても復活しない
        - 1に指すとバスが機能する
            - 一歩進んだ！
    - Raspiから蹴ってみて７セグは生きてることを確認済み
    - Raspiを左手キーボードに接続してi2cdetect -y 1して0x20にいることを確認済み
        - この時SDAが2である
        - それに合わせて配線して、i2cdetectで0x20と0x70が見つかることを確認済み

レジスタで直接LEDを操作
- LED 1 ON
    - inline void ergodox_right_led_1_on(void)    { DDRB |=  (1<<5); PORTB |=  (1<<5); }
- LED 2
    - DDRB |=  (1<<6); PORTB |=  (1<<6);
- LED 3
    - DDRB |=  (1<<7); PORTB |=  (1<<7);

ロジアナ
- 1bitずれてる



- キーマップチートシート [http://qiita.com/ReSTARTR/items/970354940f49c67fb9fd](http://qiita.com/ReSTARTR/items/970354940f49c67fb9fd)
- [https://www.pjrc.com/teensy/loader_cli.html](https://www.pjrc.com/teensy/loader_cli.html)
- ErgoDoxでマクロを使う - Qiita
    - [http://qiita.com/teri_yakichan/items/db54589b67ba9330faed](http://qiita.com/teri_yakichan/items/db54589b67ba9330faed)
- 💥🍣emojiキーを設定しよう🍣💥 - Qiita
    - [http://qiita.com/miyaoka/items/969864e5219349f01be3](http://qiita.com/miyaoka/items/969864e5219349f01be3)
- I2C
    - [https://github.com/benblazak/ergodox-firmware/blob/master/src/lib/twi/teensy-2-0.c](https://github.com/benblazak/ergodox-firmware/blob/master/src/lib/twi/teensy-2-0.c)
