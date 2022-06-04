---
description: scanning lines
---

# 閃爍條紋

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform float u_time;
uniform vec2 u_resolution;

void main(){
  vec2 coord = gl_FragCoord.xy / u_resolution;
  vec3 color = vec3(1.0);

  // 決定總共有幾格閃爍 
  float size = 6.0;
  float alpha = 0.0;

  // 1. 新增 alpha 變數 -> 可以看到畫面不停在黑與白之間閃爍
  // 4.0 數字越大 -> 閃爍越快
  alpha = sin(u_time * 4.0); 

  // 2. 沿著 y 軸進行閃爍
  // alpha = sin(floor(coord.y * size) + u_time * 4.0); 

  // 3. 後面加上常數，讓某幾列一直維持白色條紋效果
  // size = 24.0;
  // alpha = sin(floor(coord.y * size) + u_time * 4.0) + 1.0 / 2.0;

  // 4. 換成 x 軸
  // size = 24.0;
  // alpha = sin(floor(coord.x * size) + u_time * 4.0) + 1.0 / 2.0;

  gl_FragColor = vec4(color, alpha);
}
```

![](<../.gitbook/assets/image (2).png>)

### Reference

{% embed url="https://www.youtube.com/watch?index=20&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=EzYZDJKVEwE" %}
