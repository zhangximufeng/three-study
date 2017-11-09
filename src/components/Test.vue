<template>
   <div id="WebGL-output">

   </div>
  
</template>
<style>
 body {
     margin:0;
     overflow: hidden;
 }

</style>
<script>
import * as three from 'three'
export default {
  methods:{
      init(){
          console.log(three)
        //   定义场景
          var scene = new three.Scene()
        //   定义摄像机
          var camera = new three.PerspectiveCamera(60,window.innerWidth/window.innerHeight,0.1,1000)
        //   定义渲染器
          var renderer = new three.WebGLRenderer()
        //   设置场景大小
            renderer.setSize(window.innerWidth,window.innerHeight)
            // 设置场景颜色
            renderer.setClearColor(new three.Color(0xeeeeee))
        
            renderer.shadowMap.enabled = true
  

            // 添加轴
            var axes = new three.AxisHelper(20)
            scene.add(axes)
            // 添加平面
            var planeGeometry = new three.PlaneGeometry(60,20,1,1)
            var planeMaterial = new three.MeshLambertMaterial({color:0xcccccc})
            var plane = new three.Mesh(planeGeometry,planeMaterial)
            plane.rotation.x = -0.5 * Math.PI
            plane.position.x = 15
            plane.position.y = 0
            plane.position.z = 0
         
            plane.receiveShadow = true
            scene.add(plane)
            // 添加正方体
            var cubeGeometry = new three.BoxGeometry(6,6,6)
            var cubeMaterial = new three.MeshLambertMaterial({
                color:0xff0000,wireframe:false
            })
            var cube = new three.Mesh(cubeGeometry,cubeMaterial)
            cube.position.x = -6
            cube.position.y = 5
            cube.position.z = 0
            cube.castShadow = true
            scene.add(cube)
            // 添加球体
            var sphereGeometry = new three.SphereGeometry(4,20,20)
            var sphereMaterial = new three.MeshLambertMaterial({
                color:0x7777ff,wireframe:false
            })
            var sphere = new three.Mesh(sphereGeometry,sphereMaterial)
            sphere.position.x = 20
            sphere.position.y = 4
            sphere.position.z = 2
            sphere.castShadow = true
            scene.add(sphere)
            // 定义摄像机
            camera.position.x = -30
            camera.position.y = 40
            camera.position.z = 30
            // 指向 （0，0，0）
            camera.lookAt(scene.position)
            // 定义光源
            var spotLight = new three.SpotLight( 0xffffff )
          
            spotLight.position.set(-40,60,-10)
            spotLight.castShadow = true
            

            scene.add(spotLight)

            





            // 添加到dom元素中
            document.getElementById("WebGL-output").appendChild(renderer.domElement)
            renderScene()
            function renderScene(){
                requestAnimationFrame(renderScene)
                renderer.render(scene,camera)
            }
      }
  },
  mounted(){
      this.init()
  }
}
</script>
