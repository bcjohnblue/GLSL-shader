---
description: rotate
---

# 旋轉

```glsl
#ifdef GL_ES
precision mediump float;
#endif

#define PI 3.14159265359

uniform vec2 u_resolution;
uniform float u_time;

mat2 rotate2d(float angle) {
  return mat2(cos(angle), -sin(angle), sin(angle), cos(angle));
}

// scale 為寬、高
float rectshape(vec2 position, vec2 scale){
  // 以中心點為中心對各半做 scale
  // ex. scale = [1, 1] => rectshape 所有點回傳的都會是 1 => 全白
  // ex. scale = [0, 0] => rectshape 所有點回傳的都會是 0 => 全黑 
  scale = vec2(0.5) - scale * 0.5;
  // 左下角 L
  vec2 shaper = vec2(step(scale.x, position.x), step(scale.y, position.y));
  // 右上角倒 L
  shaper *= vec2(step(scale.x, 1.0 - position.x), step(scale.y, 1.0 - position.y));
  // and (&) 的意思，要符合點不落在 左下角 L 與 右上角 L 的規則
  return shaper.x * shaper.y;
}

void main(){
  vec2 position = gl_FragCoord.xy / u_resolution;

  // 不加前後的 +-0.5 的話，圖形會沿著 (0,0) 為原點旋轉
  position -= 0.5;
  position *= rotate2d(u_time);
  // 加入順逆旋轉
  // position *= rotate2d(sin(u_time) * PI);
  position += 0.5;

  float rectangle = rectshape(position, vec2(0.3, 0.3));

  vec3 color = vec3(0.0);
  // 加入背景顏色
  // color = vec3(position.x, position.y, 0.0);
  color += vec3(rectangle);
  
  gl_FragColor = vec4(color, 1.0);
}
```

### Reference

{% embed url="https://www.youtube.com/watch?index=13&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=ssqTWRQwXVo" %}

{% embed url="https://thebookofshaders.com/08?lan=ch" %}
