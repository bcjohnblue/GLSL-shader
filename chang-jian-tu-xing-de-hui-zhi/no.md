---
description: rainbow swirl
---

# 旋轉の彩虹

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform float u_time;
uniform vec2 u_resolution;

void main() {
  vec2 coord = (gl_FragCoord.xy / u_resolution);
  vec3 color = vec3(0.0);

  // 呈現旋轉
  float angle = atan(-coord.y + 0.25, coord.x - 0.5) * 0.1;
  // 這裡的數字要配合上面的數字，所有彩虹的中心才會是同一個點
  float len = length(coord - vec2(0.5, 0.25));

  // 1. 先創造出一個同心圓，數字 (小 -> 大 造成效果 zoom-in -> zoom-out) 
  // color += sin(len * 50.0);

  // 2. 加入 angle 創造出不同圓之間的切面
  // color += sin(len * 50.0 + angle);

  // 3. 將 angle 乘以一個常數，創造出旋轉的圖樣
  // 乘以的常數 40.0 -> 決定旋轉角度，旋臂也會隨著數字越大變越多條
  // color += sin(len * 50.0 + angle * 40.0);

  // 4. 加上 u_time，圖形開始會旋轉了
  // color += sin(len * 50.0 + angle * 40.0 + u_time);

  // 5. 改變成紅色
  // color.r += sin(len * 50.0 + angle * 40.0 + u_time);

  // 6. 調整改變 r, g 顏色
  // color.r += sin(len * 50.0 + angle * 40.0 + u_time);
  // color.g += cos(len * 50.0 + angle * 40.0 - u_time);

  // 7. 調整加入 b 顏色
  // color.r += sin(len * 50.0 + angle * 40.0 + u_time);
  // color.g += cos(len * 50.0 + angle * 40.0 - u_time);
  // color.b += sin(len * 50.0 + angle * 40.0 + 6.0);

  // 8. 調整 len 及 angle 乘以的常數，讓三個圓的旋轉是不重疊的，創造出旋轉彩虹效果
  color.r += sin(len * 40.0 + angle * 40.0 + u_time);
  color.g += cos(len * 30.0 + angle * 60.0 - u_time);
  color.b += sin(len * 50.0 + angle * 50.0 + 3.0);

  gl_FragColor = vec4(color, 1.0);
}
```

![](<../.gitbook/assets/image (1).png>)

### Reference

{% embed url="https://www.youtube.com/watch?index=19&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=wkWYXjrOVlA" %}
