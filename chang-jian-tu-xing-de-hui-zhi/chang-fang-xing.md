# 長方形

第一步：

先了解長方形是由繪製左下角 L與右上角倒 L 而來。

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

void main(){
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    // 繪製左下角 L
    vec2 bl = step(vec2(0.1),st);
    float pct = bl.x * bl.y;

    // 繪製右下角 L
    // vec2 tr = step(vec2(0.1),1.0-st);
    // pct *= tr.x * tr.y;

    color = vec3(pct);

    gl_FragColor = vec4(color,1.0);
}
```

第二步：

由外部傳入 scale (寬、高) 繪製長方形

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

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

	vec3 color = vec3(0.0);

	float rectangle = rectshape(position, vec2(0.3, 0.3));

	color = vec3(rectangle);

	gl_FragColor = vec4(color, 1.0);
}
```

### Reference

{% embed url="https://www.youtube.com/watch?index=9&list=PL4neAtv21WOmIrTrkNO3xCyrxg4LKkrF7&v=9oYssHkOn0I" %}

### Extended

1. 將 step 改為 smoothstep 將會有 blur 的效果

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

void main(){
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    // 繪製左下角 L
    vec2 bl = smoothstep(vec2(0.1), vec2(0.2),st);
    float pct = bl.x * bl.y;

    // 繪製右下角 L
    vec2 tr = smoothstep(vec2(0.1), vec2(0.2), 1.0-st);
    pct *= tr.x * tr.y;

    color = vec3(pct);

    gl_FragColor = vec4(color,1.0);
}
```

2\. 用 [floor](https://thebookofshaders.com/glossary/?search=floor) 改寫

基本上就是原本的 st => st + 1

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

void main(){
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec3 color = vec3(0.0);

    // 繪製左下角 L
    vec2 bl = floor(st + vec2(1.0) - vec2(0.1));
    // vec2 bl = step(vec2(0.1),st);
    float pct = bl.x * bl.y;

    // 繪製右下角 L
    vec2 tr = floor(vec2(2.0 - 0.1) - st);
    // vec2 tr = step(vec2(0.1),1.0-st);
    pct *= tr.x * tr.y;

    color = vec3(pct);

    gl_FragColor = vec4(color,1.0);
}
```
