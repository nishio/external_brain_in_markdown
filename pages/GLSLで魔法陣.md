
![image](https://gyazo.com/e2664da059d8d2ac4c165eebfc93b8b4/thumb/1000)
- [https://glslsandbox.com/e#74380.0](https://glslsandbox.com/e#74380.0)

glsl

```
#ifdef GL_ES
precision mediump float;
#endif

#extension GL_OES_standard_derivatives : enable

uniform float time;
uniform vec2 mouse;
uniform vec2 resolution;

float circle(float r, float radius, float stroke_width) {
	return (abs(r - radius) <= stroke_width) ? 1. : 0.;
}

float line(vec2 p, float y, float stroke_width){
	return abs(p.y - y) <= stroke_width ? 1. : 0.;
}

vec2 rotate(vec2 v, float th) {
	return vec2(cos(th) * v.x - sin(th) * v.y, sin(th) * v.x + cos(th) * v.y);
}

void main( void ) {
	vec2 from_center_x2 = (gl_FragCoord.xy * 2. - resolution);
	vec2 p_ = from_center_x2 / min(resolution.y, resolution.x);
	vec2 p = rotate(p_, time);
	float r = length(p);
	float f_inside = 1. - step(1., r);
	
	float f_circle = circle(r, 1.0, 0.02);
	float f_lines = 0.;
	for(int i = 0; i <3; i++){
		f_lines += line(rotate(p, 2. * 3.1415 / 3. * float(i)), 0.5,  0.01);
	}
	for(int i = 0; i <3; i++){
		f_lines += line(rotate(p, 2. * 3.1415 / 3. * (float(i) + .5)), 0.5,  0.01);
	}
	float addition = f_lines + f_circle;
	float multiplication = addition * f_inside;
	gl_FragColor=vec4(multiplication);
}
```


![image](https://gyazo.com/acb7cad77a8f762e64a948f97a2102f3/thumb/1000)
- [https://glslsandbox.com/e#74381.0](https://glslsandbox.com/e#74381.0)
glsl

```
#ifdef GL_ES
precision mediump float;
#endif

#extension GL_OES_standard_derivatives : enable

uniform float time;
uniform vec2 mouse;
uniform vec2 resolution;

float circle(float r, float radius, float stroke_width) {
	return (abs(r - radius) <= stroke_width) ? 1. : 0.;
}

float line(vec2 p, float y, float stroke_width){
	return abs(p.y - y) <= stroke_width ? 1. : 0.;
}

vec2 rotate(vec2 v, float th) {
	return vec2(cos(th) * v.x - sin(th) * v.y, sin(th) * v.x + cos(th) * v.y);
}

float hexagram(vec2 p, vec2 center, float radius, float stroke_width) {
	float r = length(p - center);
	float f_inside = 1. - step(radius, r);
	
	float f_circle = circle(r, radius, stroke_width * 2.);
	float f_lines = 0.;
	for(int i = 0; i <3; i++){
		f_lines += line(rotate(p, 2. * 3.1415 / 3. * float(i)), radius / 2.,  stroke_width);
	}
	for(int i = 0; i <3; i++){
		f_lines += line(rotate(p, 2. * 3.1415 / 3. * (float(i) + .5)), radius / 2.,  stroke_width);
	}
	float addition = f_lines + f_circle;
	float multiplication = addition * f_inside;

	return multiplication;
}

void main( void ) {
	vec2 from_center_x2 = (gl_FragCoord.xy * 2. - resolution);
	vec2 p = from_center_x2 / min(resolution.y, resolution.x);
	//vec2 p = rotate(p_, time);
	float addition = 0.;
	float radius = .8;
	float stroke_width = 0.01;
	for(int i = 0; i <10; i++){
		addition += hexagram(rotate(p, .5 * time * float(i + 1)), vec2(0., 0.), radius, stroke_width);
		radius /= 2.;
		stroke_width /= 2.;
	}
	float multiplication = addition * 1.;
	gl_FragColor=vec4(multiplication);
}
```


![image](https://gyazo.com/732e0474832a7f61cb562bf6db56c316/thumb/1000)

[https://twitter.com/nishio/status/1426457468989698048?s=21](https://twitter.com/nishio/status/1426457468989698048?s=21)
