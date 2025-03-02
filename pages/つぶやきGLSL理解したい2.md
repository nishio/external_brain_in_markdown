
![image](https://gyazo.com/d51a385cbd95bb9fa82ae8f1fd3b60b9/thumb/1000)
[https://twitter.com/zozuar/status/1377258798595895297](https://twitter.com/zozuar/status/1377258798595895297)

rotate3D
:

```
// from https://github.com/doxas/twigl
mat3 rotate3D(float angle, vec3 axis){
    vec3 a = normalize(axis);
    float s = sin(angle);
    float c = cos(angle);
    float r = 1.0 - c;
    return mat3(
        a.x * a.x * r + c,
        a.y * a.x * r + a.z * s,
        a.z * a.x * r - a.y * s,
        a.x * a.y * r - a.z * s,
        a.y * a.y * r + c,
        a.z * a.y * r + a.x * s,
        a.x * a.z * r + a.y * s,
        a.y * a.z * r - a.x * s,
        a.z * a.z * r + c
    );
}
```


:

```
out vec4 o;
```

:

```
ERROR: 0:31: 'out' : storage qualifier supported in GLSL ES 3.00 and above only
ERROR: 0:31: 'out' : Local variables can only use the const storage qualifier.
ERROR: 0:31: 'out' : invalid qualifier combination
```

- [Whats the replacement of gl_FragColor? : opengl](https://www.reddit.com/r/opengl/comments/7s2wgz/whats_the_replacement_of_gl_fragcolor/)

:

```
for(o++;i++<1e2;g+=max(.05,e*.3)){
```

:

```
ERROR: 0:38: 'for' : Invalid init declaration
```

- [javascript - webGL shader errors - Stack Overflow](https://stackoverflow.com/questions/11216912/webgl-shader-errors)
    - > In a for loop, the variable must be declared in the loop header itself, not outside:

うーん、環境が違うのかな。保留。

こちらは動く環境へのリンク付き
[https://twitter.com/zozuar/status/1379735772182511623?s=21](https://twitter.com/zozuar/status/1379735772182511623?s=21)
