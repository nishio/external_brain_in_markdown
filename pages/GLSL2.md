
![image](https://gyazo.com/f949c22f95ac7104629cc991bce2254d/thumb/1000)

:

```
#ifdef GL_ES
precision mediump float;
#endif

#extension GL_OES_standard_derivatives : enable

uniform float time;
uniform vec2 mouse;
uniform vec2 resolution;

float ball(vec2 position, float x, float y){
	return 0.8 * step(length(position - (0.3 * cos(vec2(time * x, time * y)))), 0.05);
}
void main( void ) {
	vec2 position = ( gl_FragCoord.xy / min(resolution.x, resolution.y) ) - 0.5; 
	vec4 c = vec4(0);
	float th = 1.256;
	for(int i=0; i< 5; i++){
		c += vec4(ball(position, .2, .3), 0., 0., 1.);
		c += vec4(0., ball(position, .3, .5), 0., 1.);
		c += vec4(0., 0., ball(position, .5, .7), 1.);
		c += vec4(ball(position, .7, 1.1), 0., 0., 1.);
		c += vec4(0., ball(position, 1.1, 1.3), 0., 1.);
		c += vec4(0., 0., ball(position, 1.3, 1.7), 1.);
		position = mat2(cos(th), -sin(th), sin(th), cos(th)) * position;
	}
	gl_FragColor = vec4(c);
}
```


:

```
#define b(p,x,y) .8*step(length(p-(.3*cos(vec2(time*x,time*y)))),.05)

void main( void ) {
	vec2 r=resolution;
	vec2 p=(gl_FragCoord.xy/min(r.x,r.y))-.5;
	vec4 c=vec4(0);
	float a=1.256,x=cos(a);
	for(int i=0;i<5;i++){
		c+=vec4(b(p,.2,.3)+b(p,.7,1.1),b(p,.3,.5)+b(p,1.1,1.3),b(p,.5,.7)+b(p,1.3,1.7),1);
		p*=mat2(cos(a), -sin(a), sin(a), cos(a));}
	gl_FragColor=c;
}
```


:

```
#ifdef GL_ES
precision mediump float;
#endif

#extension GL_OES_standard_derivatives : enable

uniform float time;
uniform vec2 mouse;
uniform vec2 resolution;

#define b(p,x,y) .8*step(length(p-(.3*cos(time*vec2(x,y)))),.05)

void main( void ) {
	vec2 r=resolution;
	vec2 p=(gl_FragCoord.xy/min(r.x,r.y))-.5;
	vec4 c=vec4(0);
	for(int i=0;i<5;i++){
		c+=vec4(b(p,.2,.3)+b(p,.7,1.1),b(p,.3,.5)+b(p,1.1,1.3),b(p,.5,.7)+b(p,1.3,1.7),1);
		p*=mat2(cos(vec4(93,60,82,93)));}
	gl_FragColor=c;
}
```

[http://glslsandbox.com/e#72260.0](http://glslsandbox.com/e#72260.0)
