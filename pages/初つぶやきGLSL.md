
![image](https://gyazo.com/88943837591a00a7cca1196a898ac04f/thumb/1000)
[http://glslsandbox.com/e#72258.0](http://glslsandbox.com/e#72258.0)

:

```
#ifdef GL_ES
precision mediump float;
#endif

#extension GL_OES_standard_derivatives : enable

uniform float time;
uniform vec2 mouse;
uniform vec2 resolution;
#define PI 3.1415926535897932384626433832795

void main( void ) {
	float t = time / PI;
	mat2 m = mat2(cos(t), -sin(t), sin(t), cos(t));
	if(fract(t / PI / 2.) < .5){
		vec2 p = fract( gl_FragCoord.xy / min(resolution.x, resolution.y) * 10. ) - 0.5;
		p = m * p;
		vec2 p2 = abs(p);
		float c = step(p2.x + p2.y, .5);
		gl_FragColor = vec4( c );
	}else{	
		vec2 p = fract( gl_FragCoord.xy / min(resolution.x, resolution.y) * 10. + .5) - 0.5;
		p = m * p;
		vec2 p2 = abs(p);
		float c = step(0.5, p2.x + p2.y);
		gl_FragColor = vec4( c );
	}
}
```


:

```
void main( void ) {
	float t = time;
	vec2 r = resolution;
	mat2 m = mat2(cos(t), -sin(t), sin(t), cos(t));
	vec2 a=gl_FragCoord.xy / min(r.x, r.y) * 10.;
	float c;
	bool b = fract(t / PI / 2.) < .5;
	vec2 p = fract( a + (b ? 0.:.5)) - 0.5;
	vec2 p2 = abs(m * p);
	if(b){
		c = step(p2.x + p2.y, .5);
	}else{	
		c = step(.5, p2.x + p2.y);
	}
	gl_FragColor = vec4( c );
}
```


:

```
void main( void ) {
	float t = time;
	vec2 r = resolution;
	mat2 m = mat2(cos(t), -sin(t), sin(t), cos(t));
	vec2 a=gl_FragCoord.xy / min(r.x, r.y) * 10.;
	float c;
	bool b = fract(t / PI / 2.) < .5;
	vec2 p = fract( a + (b ? 0.:.5)) - 0.5;
	vec2 p2 = abs(m * p);
	c = step(p2.x + p2.y, .5);
	c = b?c:1.-c;
	gl_FragColor = vec4( c );
}
```


:

```
void main() {
	float t = time;
	vec2 r = resolution;
	bool b=fract(t/atan(0.,-1.)/2.)<.5;
	vec2 a=gl_FragCoord.xy/min(r.x,r.y)*10.,p=fract(a+(b?0.:.5))-.5,q=abs(mat2(cos(t),-sin(t),sin(t),cos(t))*p);
	float c=step(q.x+q.y,.5);
	gl_FragColor=vec4(b?c:1.-c);
}
```


[http://glslsandbox.com/e#72258.0](http://glslsandbox.com/e#72258.0)
[https://twitter.com/nishio/status/1378229696094085123](https://twitter.com/nishio/status/1378229696094085123)
