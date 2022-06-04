---
description: Translation
---

# 平移

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

float circleshape(vec2 position, float radius){
  // 小於 radius 的都回傳 0，大於 radius 的都回傳 1
  return step(radius, length(position));
}

void main(){
  vec2 position = gl_FragCoord.xy / u_resolution; // 0.0 - 1.0
  // 置中 
  // position -= 0.5; // -0.5 - 0.5

  // 平移 (與上面置中為同一效果)
  vec2 translate = vec2(-0.5, -0.5);
  position += translate;

  // 校正橢圓 to 圓形
  position.x *= u_resolution.x / u_resolution.y;
  
  float circle = circleshape(position, 0.2);

  vec3 color = vec3(0.0);
  color = vec3(circle);

  gl_FragColor = vec4(color, 1.0);
}
```

### Reference

{% embed url="https://www.youtube.com/watch?index=10&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=dQ2XDN5r9Nc" %}
