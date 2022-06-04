---
description: 內建函式
---

# sine/cosine

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

float circleshape(vec2 position, float radius){
  // 小於 radius 的都回傳 0，大於 radius 的都回傳 1
  return step(radius, length(position));
}

void main(){
  vec2 position = gl_FragCoord.xy / u_resolution; // 0.0 - 1.0

  // 利用 sine/consine 移動 x, y 軸
  vec2 translate = vec2(0, 0);
  translate = vec2(sin(u_time), 0);
  // translate = vec2(sin(u_time / 10.), 0);
  // translate = vec2(sin(u_time / 10.), cos(u_time));

  position += translate * 0.5 - 0.5;

  // 校正橢圓 to 圓形
  position.x *= u_resolution.x / u_resolution.y;
  
  float circle = circleshape(position, 0.3);

  vec3 color = vec3(0.0);
  color = vec3(circle);

  gl_FragColor = vec4(color, 1.0);
}
```

### Reference

{% embed url="https://www.youtube.com/watch?index=11&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=meeNZQNxbeQ" %}
