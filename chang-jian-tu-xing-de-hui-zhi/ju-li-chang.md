---
description: Distance Field
---

# 距離場

可以創造出重複圖案

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

void main(){
  vec2 st = gl_FragCoord.xy/u_resolution.xy; // 0 ~ 1
  st.x *= u_resolution.x/u_resolution.y;
  vec3 color = vec3(0.0);
  float d = 0.0;

  // Remap the space to -1. to 1.
  st = st * 2. - 1.; // -1 ~ 1

  // Make the distance field
  // 代表距離 0.3 點的距離，因為用了 abs，平面上會有四個點與 0.3 的距離都為 0 (黑色)
  d = length( abs(st)-.3 );
  
  // 距離大於 0.3 的點都會是 0，即大於 0.3 距離的地方都會是黑色 
  // d = length( min(abs(st)-.3,0.) );
  
  // 距離小於 0.3 的點都會是 0，即小於 0.3 距離的地方都會是黑色 (中間為黑色正方形)
  // d = length( max(abs(st)-.3,0.) );

  // Visualize the distance field
  // 利用 fract 讓整個重複的圖樣更明顯
  gl_FragColor = vec4(vec3(fract(d*10.0)),1.0);

  // Drawing with the distance field
  
  // 小於 0.3 為 0 (黑色)
  // gl_FragColor = vec4(vec3( step(.3,d) ),1.0);
  
  // 小於 0.3 為 0 (黑色)，大於 0.3 小於 0.4 為 1 (白色)，大於 0.4 為 0 (黑色)
  // gl_FragColor = vec4(vec3( step(.3,d) * step(d,.4)),1.0);
  
  // 利用 smoothstep 製造與上面相同但模糊效果
  // gl_FragColor = vec4(vec3( smoothstep(.3,.4,d)* smoothstep(.6,.5,d)) ,1.0);
}
```



### Reference

{% embed url="https://thebookofshaders.com/07" %}
