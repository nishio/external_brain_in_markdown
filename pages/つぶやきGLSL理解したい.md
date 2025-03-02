
from [[つぶやきGLSL]]

これを理解したい
- [https://twitter.com/setchi/status/1251153387187367939](https://twitter.com/setchi/status/1251153387187367939)
glsl

```
void main(){vec2 p=(.5-fract(mat2(cos(-t*.4+vec4(1,33,11,1)))*(gl_FragCoord.xy*2.-r)/min(r.y,r.x)))*2.4;float q=length(p),a=atan(p.y,p.x)*2.5+t*2.;gl_FragColor=vec4(mix(q*.9*step(q,min(abs(sin(a))+.4,abs(cos(a))+1.1)*.7),.7,step(q,.15)));}
```

- ![image](https://gyazo.com/c886047f75a75510549a8c65963f2fe2/thumb/1000)

どうやって動かすのか
- GLSL Sandboxってのがあるらしい
- [GLSL Sandboxで遊ぼう | notargs.com](http://wordpress.notargs.com/blog/blog/2015/02/25/glsl-sandbox%e3%81%a7%e9%81%8a%e3%81%bc%e3%81%86/)
- エラーメッセージはどうやって見るのか
    - コンソールに出てた
- tとrをtimeとresolutionに変更したら動いた
    - ![image](https://gyazo.com/a6858f7a158d6989efc49e5cabe03527/thumb/1000)

[OpenGL 4.x Reference Pages](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/indexflat.php)
- [step - OpenGL 4 Reference Pages](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/step.xhtml)
    - `step(edge, x) == x < edge ? 0.0 : 1.0`
- [fract - OpenGL 4 Reference Pages](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fract.xhtml)
    - `x - floor(x)`
- [mix - OpenGL 4 Reference Pages](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mix.xhtml)
    - `mix(x, y, a) == x * (1 - a) + y * a`

時間による拡大縮小部分
:

```
mat2(
    cos(-time * .4 + vec4(1,33,11,1))
) 
```


タイリング
:

```
vec2 from_center_x2 = (gl_FragCoord.xy * 2. - resolution);
vec2 p1 = from_center_x2 / min(resolution.y, resolution.x); 
vec2 p2 = fract(p1); 
vec2 p=( .5 - p2 ) * 2.4;
```

- ![image](https://gyazo.com/ed45b38029f2e1c4b187beb7b7da4d4c/thumb/1000)

中心からの距離
:

```
float q=length(p);
```


中心からの角度
- 2.5倍しているので、一周で5π、これが花びらの枚数になる。時刻を足しているので時間経過で回転する
:

```
float a=atan(p.y, p.x) * 2.5 + time * 2.;
```


step(q, edge)
- 「中心からの距離がedge以下なら1.0」ということなので中心付近を塗るのに使える

輪郭の形
:

```
min(abs(sin(a))+.4, abs(cos(a))+1.1) 
```

- ![image](https://gyazo.com/87926436442193a2483cc6801bd1499d/thumb/1000)

中心からの距離に応じたグラデーション
:

```
q * .9 * step( ... )
```


これは中央の丸
:

```
step(q,.15)
```


yが固定のmixは何か
- aが0の時x、1の時y、という条件分岐

拡大縮小部分のコード
:

```
mat2 m = mat2(cos(-time * .4 + vec4(1,33,11,1)));
vec2 p2 = fract(m * p1);
```

- 33などのマジックナンバー
    - どうせcosに入れるので2πの倍数には意味がない
    - 計算してみるとπ/2の倍数に近い値
    - ショートコーディングのためのテクニックに過ぎない
    - 下記のコードと振る舞いは同じ
:

```
float pi = 3.14159;
mat2 m2 = mat2(
  cos(-.4 * time + 1.), 
  cos(-.4 * time + pi * 0.5), 
  cos(-.4 * time + pi * 1.5),
  cos(-.4 * time + 1.));
vec2 p2 = fract(m2 * p1);
```

    - sinも使うとこうなる
:

```
float t = -.4 * time;
mat2 m2 = mat2(cos(t + 1.), -sin(t), sin(t), cos(t + 1.));
vec2 p2 = fract(m2 * p1);
```

        - cosに対する+1.がなければ単なる回転になる

ここまでを踏まえて少し改造した
- ![image](https://gyazo.com/c42b981ccaaa5d56e2052158edb93102/thumb/1000)
- [http://glslsandbox.com/e#72257.0](http://glslsandbox.com/e#72257.0)
