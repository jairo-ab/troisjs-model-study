
<script>
// Model from mixamo.com
import { AnimationMixer, Clock, Fog, GridHelper, Vector3 } from 'three';
import {
  AmbientLight,
  Camera,
  DirectionalLight,
  FbxModel,
  HemisphereLight,
  Renderer,
  PhongMaterial,
  Plane,
  Scene,
  Texture,
  StandardMaterial
} from 'troisjs';
export default {
  components: {
    AmbientLight,
    Camera,
    DirectionalLight,
    FbxModel,
    HemisphereLight,
    Renderer,
    PhongMaterial,
    Plane,
    Scene,
    Texture,
    StandardMaterial
  },
  data() {
    return {
      target: new Vector3(0, 100, 0),
    };
  },
  mounted() {
    const scene = this.$refs.scene.scene;
    scene.fog = new Fog(0xa0a0a0, 200, 1000);
    const grid = new GridHelper(2000, 20, 0x000000, 0x000000);
    grid.material.opacity = 0.5;
    grid.material.transparent = true;
    this.$refs.scene.add(grid);

    responsiveVoice.setDefaultRate(1.5);
    responsiveVoice.speak("Olá Hugo, seja bem-vindo a samel. Identificamos que você tem uma consulta com o cardiologista Paulo César, deseja fazer o Check-in dessa consulta? Diga Sim para realizar o Check-in, ou não para sair","Brazilian Portuguese Female", { rate: 1})
  },
  methods: {
    onLoad(object) {

      this.mixer = new AnimationMixer(object);
      const action = this.mixer.clipAction(object.animations[0]);
      action.play();
      
      object.traverse(child => {
        if (child.isMesh) {
          child.castShadow = true;
          child.receiveShadow = true;
        }
      });
      this.clock = new Clock();
      this.$refs.renderer.onBeforeRender(this.updateMixer);
    },
    updateMixer() {
      this.mixer.update(this.clock.getDelta());
    },
  },
};
</script>

<template>
  <Renderer ref="renderer" :orbit-ctrl="{ enableDamping: true, target }" antialias  resize shadow>
    <Camera :position="{ x: 0, y: 150, z: 500 }" />
    <Scene ref="scene" background="#757575">
      <HemisphereLight />

        <DirectionalLight
          :position="{ x: 0, y: 200, z: 100 }"
          cast-shadow :shadow-camera="{ top: 180, bottom: 120, left: 120, right: 120 }"
        />

      <Plane :width="2000" :height="2000" :rotation="{ x: -Math.PI / 2 }" receive-shadow>
        <PhongMaterial color="#999999" :props="{ depthWrite: false }" />
      </Plane>

      <FbxModel src="/models/Samba.fbx" @load="onLoad" />
    </Scene>
  </Renderer>
</template>