---
description: 圓形
---

# 圓形

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

float circleshape(vec2 position, float radius){
  // 小於 radius 的都回傳 0，大於 radius 的都回傳 1
  return step(radius, length(position));
  // 可以利用 smoothstep 將邊緣模糊化
  // return smoothstep(radius - (radius * 0.01), radius + (radius * 0.01), length(position));
}

void main(){
  vec2 position = gl_FragCoord.xy / u_resolution; // 0.0 - 1.0
  // 置中 
  position -= 0.5; // -0.5 - 0.5
  // 校正橢圓 to 圓形
  position.x *= u_resolution.x / u_resolution.y;

  vec3 color = vec3(0.0);
  
  float circle = circleshape(position, 0.2);

  color = vec3(circle);

  gl_FragColor = vec4(color, 1.0);
}
```

### Reference

{% embed url="https://www.youtube.com/watch?index=9&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=9oYssHkOn0I" %}
