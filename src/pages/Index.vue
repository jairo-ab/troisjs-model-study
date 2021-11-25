
<script lang="ts"> 
import { defineComponent, ref, onMounted } from "vue";
import { Renderer, Scene, Camera, PointLight, AmbientLight, GltfModel, Texture, FbxModel, HemisphereLight } from 'troisjs'
export default defineComponent({
    components: {
        Renderer, Scene, Camera, PointLight, AmbientLight, GltfModel, Texture, FbxModel, HemisphereLight
    },
    setup() {
        const renderer = ref(null);
        const model = ref(null);
        
        onMounted(() => {
            renderer?.value?.onBeforeRender(() => {
                model.value.rotation.x += 0.01;
            });

            Scene.background = ("https://threejs.org/examples/textures/uv_grid_opengl.jpg");

            responsiveVoice.setDefaultRate(1.5);
            responsiveVoice.speak("Mensagem","Brazilian Portuguese Male", { rate: 1})
        })

        function onReady(model) {
            model.traverse(o => {
                if (o.isMesh) {
                // handle both multiple and single materials
                    const asArray = Array.isArray(o.material) ? o.material : [o.material]
                    // 0 works for matte materials - change as needed
                    asArray.forEach(mat => (mat.metalness = 0))
                }
            })
        }

        return {
            renderer,
            model,
            onReady,
        }
    }
})
</script>

<template>
    <div class="container">
        <Renderer ref="renderer" antialias :orbit-ctrl="{ enableDamping: true, dampingFactor: 0.05, autoRotate: false }" shadow resize="window">
            <Camera :position="{x: 0, y: 5, z: 250}" />
            <Scene background="#a0a0a0">
                <AmbientLight />
                <HemisphereLight />
                <PointLight
                color="white"
                :position="{ x: 50, y: -20, z: 40 }"
                :intensity="2"
                />
                <!--<GltfModel
                    ref="model"
                    src="/models/robo_caixa/scene.gltf"
                    @load="onReady"
                />-->
                <FbxModel ref="model" src="/models/robot/SambaDancing.fbx" @load="onReady" />
            </Scene>
        </Renderer>
    </div>
</template>


<style scoped>
    .container {
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>