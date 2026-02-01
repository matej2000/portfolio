<!-- <script setup>
import { shallowRef } from 'vue'
import { useLoop } from '@tresjs/core'

const createCircleTexture = () => {
  const canvas = document.createElement('canvas')
  canvas.width = 64
  canvas.height = 64
  const ctx = canvas.getContext('2d')

  // Draw a radial gradient: white in middle, transparent at edges
  const gradient = ctx.createRadialGradient(32, 32, 0, 32, 32, 32)
  gradient.addColorStop(0, 'rgba(255, 255, 255, 1)')
  gradient.addColorStop(1, 'rgba(255, 255, 255, 0)')

  ctx.fillStyle = gradient
  ctx.fillRect(0, 0, 64, 64)

  const texture = new THREE.CanvasTexture(canvas)
  return texture
}

//const circleTexture = createCircleTexture()

const knotRef = shallowRef()
const { onBeforeRender } = useLoop()

onBeforeRender(({ delta, elapsed }) => {
//   if (knotRef.value) {
//     knotRef.value.rotation.x += delta * 0.2
//     knotRef.value.rotation.y += delta * 0.3
//   }
    knotRef.value.position.y = Math.sin(elapsed*2) * 0.2
    knotRef.value.rotation.z += delta * 0.2
})
</script> -->

<!-- <template>
  <TresPoints ref="knotRef">
    <TresTorusKnotGeometry :args="[3, 0.8, 256, 32, 3, 4]" />
    <TresPointsMaterial 
      :size="0.2" 
      color="#4f46e5" 
      :transparent="true" 
      :opacity="0.1"
      :map="circleTexture"
      :alphaTest="0.01"
      :depthWrite="false"
      :sizeAttenuation="true"
      :blending="2" 
      vetexColors: true
    />
  </TresPoints>
</template> -->

<template>
  <TresPoints :position="[0, 2, 0]">
    <TresTorusKnotGeometry :args="[3, 0.8, 256, 32]" />
    <TresShaderMaterial 
      :vertexShader="vShader" 
      :fragmentShader="fShader" 
      :uniforms="uniforms"
      :transparent="true"
      :blending="2"
    />
  </TresPoints>
</template>

<script setup>
import * as THREE from 'three'
import { reactive } from 'vue'
import { useLoop} from '@tresjs/core'


const uniforms = {
  uTime: { value: 0 },
  uColor: { value: new THREE.Color('#4f46e5'),
   }
}

// Update uTime every frame to animate the shader
const { onBeforeRender } = useLoop()
onBeforeRender(({ delta, elapsed }) => {
  uniforms.uTime.value = elapsed
})

// Handles the position of each point. Use this to make points wave, pulse, or explode.
const vShader = `
  varying float vHighlight;
  uniform float uTime;

  void main() {
    // 1. Calculate the angle around the center (Mexican Wave logic)
    float angle = atan(position.y, position.x);
    
    // 2. Create the continuous wave
    // Frequency: 3.0 (how many 'heads' the worm has)
    // Speed: uTime * 4.0
    float wave = sin(angle * 3.0 + position.z * 0.5 - uTime * 4.0);
    
    // 3. Narrow the wave so it looks like a sharp "pulse" moving through
    vHighlight = pow(wave * 0.5 + 0.5, 10.0); 

    vec4 mvPosition = modelViewMatrix * vec4(position, 1.0);
    
    // Make the wave points significantly bigger
    gl_PointSize = (30.0 + (vHighlight * 80.0)) * (1.0 / -mvPosition.z);
    // gl_PointSize = (10.0 + (vHighlight *1000.0)) * (1.0 / -mvPosition.z);

    
    gl_Position = projectionMatrix * mvPosition;
  }
`

const fShader = `
  varying float vHighlight;
  uniform vec3 uColor;
  uniform vec3 uWormColor;

  void main() {
    float dist = distance(gl_PointCoord, vec2(0.5));
    if (dist > 0.5) discard;

    // Soft glow effect
    float alpha = 1.0 - smoothstep(0.4, 0.5, dist);

    // Mix colors based on the highlight
    vec3 finalColor = mix(uColor, uWormColor, vHighlight);
    
    // High brightness for the peak of the wave
    float finalAlpha = mix(0.1, 1.0, vHighlight) * alpha;

    //vec3 bloomColor = finalColor * (1.0 + vHighlight * 5.0);

    gl_FragColor = vec4(finalColor, finalAlpha);
  }
`
</script>
