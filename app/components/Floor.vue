<script setup>
import * as THREE from 'three'
import { useLoop } from '@tresjs/core'

const uniforms = {
  uTime: { value: 0 },
  uGridColor: { value: new THREE.Color('#17315c') },
  uLineThickness: { value: 0.02 },
  uBackgroundColor: {value: new THREE.Color('#080d23')}
}

const { onBeforeRender } = useLoop()
onBeforeRender(({ delta, elapsed }) => {
  uniforms.uTime.value = elapsed
})

const vShader = `
  varying vec2 vUv;
  void main() {
    vUv = uv;
    gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 2.0);
  }
`

const fShader = `
  varying vec2 vUv;
  uniform float uTime;
  uniform vec3 uGridColor; 
  uniform float uLineThickness;
  uniform vec3 uBackgroundColor; // Fixed: changed to vec3 and added semicolon

  void main() {
    vec2 grid = fract(vUv * 40.0);
    float lineX = step(grid.x, uLineThickness) + step(1.0 - uLineThickness, grid.x);
    float lineY = step(grid.y, uLineThickness) + step(1.0 - uLineThickness, grid.y);
    float gridLine = clamp(lineX + lineY, 0.0, 1.0);

    // Fixed: added semicolon and used correct vec3 type
    vec3 backgroundColor = uBackgroundColor; 

    float pulse = sin(vUv.y * 10.0 - uTime * 2.0) * 0.5 + 0.5;
    
    // Tip: I added the pulse back here so the lines actually "glow"
    // vec3 animatedLineColor = uGridColor + (pulse * 0.4);
    vec3 animatedLineColor = uGridColor;

    vec3 finalColor = mix(backgroundColor, animatedLineColor, gridLine);

    float fade = 1.0 - smoothstep(0.0, 0.7, distance(vUv, vec2(0.5)));

    // gl_FragColor = vec4(finalColor, fade);
    gl_FragColor = vec4(finalColor, fade);
  }
`
</script>

<template>
  <TresMesh :rotation="[-Math.PI / 2, 0, 0]" :position="[0, -4, 0]">
    <TresPlaneGeometry :args="[200, 200]" />
    <TresShaderMaterial 
      :vertexShader="vShader" 
      :fragmentShader="fShader" 
      :uniforms="uniforms"
      :transparent="true"
      :side="THREE.DoubleSide"
    />
  </TresMesh>
</template>