<template>
  <div class="home" fill>
    <canvas id="renderCanvas"/>
  </div>
</template>

<script>
import * as BABYLON from 'babylonjs';
export default {
    name: 'Home',
    mounted() {
        let canvas = document.getElementById("renderCanvas")
        let engine = new BABYLON.Engine(canvas,true)
        let scene = new BABYLON.Scene(engine)

        let camera = new BABYLON.ArcRotateCamera(
            "Camera", 1,2,20,
            new BABYLON.Vector3(0,0,0),
            scene
        )

        let light0 = new BABYLON.PointLight(
            "Omni",
            new BABYLON.Vector3(0,0,10),
            scene
        )

        let box = BABYLON.Mesh.CreateBox("Box", 1, scene)
        box.position.z = 2
        let plane = BABYLON.Mesh.CreatePlane("Plane", 10.0, scene)
        plane.rotation.y = Math.PI

        scene.activeCamera.attachControl(canvas)

        engine.runRenderLoop(()=>{
            scene.render()
        })

        window.addEventListener('resize', () => {
            engine.resize()
        })
    }
}
</script>
<style lang="scss">
    #renderCanvas{
        width: 1000px;
        height: 800px;
    }
</style>