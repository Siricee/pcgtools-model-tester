# My FrontEnd Playground

This is a Experimental Playground for testing demos and effects.

[![Netlify Status](https://api.netlify.com/api/v1/badges/391d9075-3341-486c-b961-2e230ff49087/deploy-status)](https://app.netlify.com/sites/sirice-playground/deploys)

## Cover Reference

- Distorted Map: https://codepen.io/supah/pen/gdegrW

- [unused] Background Image: https://codepen.io/phillip-gimmi/pen/XWOdEMW

## Sample Reference

标题动画：Titles in-view reveal: https://codepen.io/supah/pen/jvmoBE

Case Study: Design Embraced Portfolio – 2024 | Codrops
https://tympanus.net/codrops/2024/03/21/case-study-design-embraced-portfolio-2024/

Outline Sample: https://codesandbox.io/p/sandbox/edgesgeometry-iup24

mesqme/waterfalls: https://github.com/mesqme/waterfalls

https://gotohiroki.github.io/distorted-curve-slider/dist/

https://codepen.io/alphardex/pen/MWvadVW

List Hover Image Ripple: https://codepen.io/alphardex/pen/bGZJzNN

codesandbox: https://codesandbox.io/s/webgl-plane-curl-57l7h2?from-embed

Horizontal smooth-scrollbar with mousewheel: https://codepen.io/supah/pen/vvNmOr

https://github.com/devloop01/webgl-image-interactions-aristide

WebGL Structure & Tyndall Effect: [nemutas/light-shaft](https://github.com/nemutas/light-shaft) [Preview](https://nemutas.github.io/light-shaft/)

[michalzalobny/webgl-3d-engine: WebGL2 3D Engine built from scratch.](https://github.com/michalzalobny/webgl-3d-engine)

WebGPU Structure: [neuroprod/webgpu: webgpu game](https://github.com/neuroprod/webgpu)

液态图片：gotohiroki/homunculus: https://github.com/gotohiroki/homunculus
Live: https://gotohiroki.github.io/homunculus/dist/


球形玻璃：gotohiroki/ha-labo-2d https://github.com/gotohiroki/ha-labo-2d
Live: https://gotohiroki.github.io/ha-labo-2d/dist/

X 上的 Karim Maaloul：Fire Shader. I needed a fire shader in The Cursed Library, so I thought it would be interesting to deconstruct the techniques behind. Made with @threejs and custom shaders. / X
https://twitter.com/yakudoo/status/1786372418027626885 Codepen: https://codepen.io/Yakudoo/pen/ZEZWKJy

tsherif/webgl2examples: Rendering algorithms implemented in raw WebGL 2.
https://github.com/tsherif/webgl2examples

水面和天空盒融合效果不错: [jbouny/ocean: Realistic water shader for Three.js](https://github.com/jbouny/ocean)


Volumetric Clouds 体积云示例

   - [webgl-clouds - nodebox - CodeSandbox](https://codesandbox.io/p/sandbox/webgl-clouds-ut1kup) - Reference: [X 上的 Cody Bennett / X](https://x.com/Cody_J_Bennett/status/1523823691611742208)

   - [Staging / Clouds - Two Clouds ⋅ Storybook](https://github.com/pmndrs/drei-vanilla/blob/main/src/core/Cloud.ts) - [Live](https://pmndrs.github.io/drei-vanilla/?path=/story/staging-clouds--cloud-story)

   - [FarazzShaikh/three-volumetric-clouds](https://github.com/FarazzShaikh/three-volumetric-clouds)

   - Blog: [Real-time dreamy Cloudscapes with Volumetric Raymarching - The Blog of Maxime Heckel](https://blog.maximeheckel.com/posts/real-time-cloudscapes-with-volumetric-raymarching/)

   - [clouded Fuji - MONKEY CIRCUS おさるサーカス](https://mameson.com/experiment/glsl/clouded_fuji/clouded_fuji.html) - [Tweet](https://x.com/mamesoncom/status/1850568996871110929)

油画shader [On Crafting Painterly Shaders - The Blog of Maxime Heckel](https://blog.maximeheckel.com/posts/on-crafting-painterly-shaders/)

同一个模型的不同显示效果示例 https://threepipe.org/examples/#custom-pipeline/

[【Unity Shader】星河地面 ](https://zhuanlan.zhihu.com/p/1892533542233298372)

天空盒CubeTexture映射 https://github.com/kbhokray/js-skybox-mapping

## Components

- [three-stdlib](https://github.com/pmndrs/three-stdlib)
- [ViewHelper](https://github.com/sengchor/kokraf/blob/dev/js/helpers/ViewHelper.js)

## Docs

tween.js 用户指南
https://tweenjs.github.io/tween.js/docs/user_guide_zh-CN.html

VFX-JS: WebGL Effects Made Easy | Codrops
https://tympanus.net/codrops/2025/01/20/vfx-js-webgl-effects-made-easy/

Threejs built-in GLSL variables document
https://threejs.org/docs/index.html#api/en/renderers/webgl/WebGLProgram

## Code Snippets

### Shader Image Cover Setting

reference: Flag/fragmentShader.glsl.js

```glsl
 precision highp float;

 uniform vec2 size;
 uniform vec2 sizeImage;
 uniform sampler2D u_image;

 varying vec2 vUv;
 varying float vPos;

 // texture size: cover
 vec4 coverTexture(sampler2D tex, vec2 imgSize, vec2 ouv) {
   vec2 s = size;
   vec2 i = imgSize;

   float rs = s.x / s.y;
   float ri = i.x / i.y;
   vec2 new = rs < ri ? vec2(i.x * s.y / i.y, s.y) : vec2(s.x, i.y * s.x / i.x);
   vec2 offset = (rs < ri ? vec2((new.x - s.x) / 2.0, 0.0) : vec2(0.0, (new.y - s.y) / 2.0)) / new;
   vec2 uv = ouv * s / new + offset;
	
   return texture2D(tex, uv);
 }

 void main() {
   
   gl_FragColor = texture2D(u_image, vUv); // uv mapping directly
   gl_FragColor = coverTexture(u_image, sizeImage, vUv); // uv mapping with image cover.
 }
```

another sample - Simple texture webgl background size cover: https://codepen.io/supah/details/VJGmvb 


