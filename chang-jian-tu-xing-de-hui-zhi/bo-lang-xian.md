---
description: wave draw lines
---

# 波浪線

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform float u_time;
uniform vec2 u_resolution;

void main(){
  vec2 coord = (gl_FragCoord.xy / u_resolution);
  float color = 0.0;

  // 1. 由左至右漸層 (暗->亮)
  color += sin(coord.x) * 0.5; // sin(0.0) = 0; sin(1.0) = 0.84147
  gl_FragColor = vec4(vec3(color, color, color), 1.0);

  // 2. 加入一些左右晃動的垂直線條 
  // sin(u_time + coord.y * 1.) -> 白色線條的左右晃動
  // color += sin(coord.x * 6.0 + sin(u_time + coord.y * 1.)) * 0.5;
  // gl_FragColor = vec4(vec3(color, color, color), 1.0);

  // 3. 將白色線條變成鋸齒狀
  // coord.y * 1. -> coord.y * 90.0
  // color += sin(coord.x * 6.0 + sin(u_time + coord.y * 90.0 + cos(coord.x))) * 0.5;
  // gl_FragColor = vec4(vec3(color, color, color), 1.0);

  // 4. 將鋸齒狀線條加入波浪效果
  // cos(coord.x * 30.0 + u_time * 2.0)
  // color += sin(coord.x * 6.0 + sin(u_time + coord.y * 90.0 + cos(coord.x * 30.0 + u_time * 2.0))) * 0.5;
  // gl_FragColor = vec4(vec3(color, color, color), 1.0);

  // 5. 添加顏色
  // color += sin(coord.x * 6.0 + sin(u_time + coord.y * 90.0 + cos(coord.x * 30.0 + u_time * 2.0))) * 0.5;
  // gl_FragColor = vec4(vec3(color + coord.x, color + coord.x, color), 1.0);
}
```

![](<../.gitbook/assets/image (5).png>)

### Reference

{% embed url="https://www.youtube.com/watch?index=18&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=LboRu2kLQR4" %}
