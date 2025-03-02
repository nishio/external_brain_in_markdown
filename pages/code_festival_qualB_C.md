
[C - 錬金術士](https://atcoder.jp/contests/code-festival-2014-qualb/tasks/code_festival_qualB_c)
- ![image](https://gyazo.com/af3c304e49c0ad7075a784961cdcaf35/thumb/1000)
- 考えたこと
    - まあ文字列の順番は関係ないのでまず頻度表にはするだろう
    - 各文字について
        - 需要量よりS1での供給量が少ないなら、差はS2から取らなければならない。逆も同様。
        - この「取る文字数」を積算して、Nを超えたらNG
        - 超えなかったらOKと言えるのか？
            - 特に反例は思いつかないが…
        - 超えない場合ってのは、残りの文字はS1にもS2にもあってどちらからとっても良いということ
            - だからOK

- 公式解説なし
