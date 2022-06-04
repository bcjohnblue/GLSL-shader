---
description: scale
---

# 縮放

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

mat2 scale(vec2 scale){
  return mat2(scale.x, 0.0, 0.0, scale.y);
}

float circleshape(vec2 position, float radius){
  // 小於 radius 的都回傳 0，大於 radius 的都回傳 1
  return step(radius, length(position));
}

void main(){
  vec2 position = gl_FragCoord.xy / u_resolution; // 0.0 - 1.0
  position -= 0.5;

  // scale
  // 以下兩行等價
  position *= scale(vec2(sin(u_time) + 2.));
  // position *= vec2(sin(u_time) + 2.);

  // 校正橢圓 to 圓形
  position.x *= u_resolution.x / u_resolution.y;
  
  float circle = circleshape(position, 0.3);

  vec3 color = vec3(0.0);
  color = vec3(circle);

  gl_FragColor = vec4(color, 1.0);
}
```

### Mat2 運算

```glsl
vec2 a = vec2(1., 2.);
mat2 b = mat2(1., 2., 3., 4.);
vec2 c = a * b // = vec2(1. * 1. + 3. * 2., 2. * 1. + 4. * 2.) = vec2(7, 10)
```

### ![](<../.gitbook/assets/image (4).png>)= \[7, 10]

### Reference

{% embed url="https://www.youtube.com/watch?index=12&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=gxOfjRT5CMA" %}

{% embed url="https://thebookofshaders.com/08?lan=ch" %}
