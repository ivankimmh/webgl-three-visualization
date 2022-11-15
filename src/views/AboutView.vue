// 강사님 코드

<template>
  <div class="container"></div>
</template>

<script>
import * as THREE from 'three'
// import { RectAreaLightHelper } from 'three/examples/jsm/helpers/RectAreaLightHelper'
// import { RectAreaLightUniformsLib } from 'three/examples/jsm/lights/RectAreaLightUniformsLib'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import * as dat from 'dat.gui'
import Stats from 'three/examples/jsm/libs/stats.module'
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader.js'

export default {
  name: 'AboutView',
  async mounted() {
    const scene = new THREE.Scene()

    scene.background = new THREE.Color(0x555555)

    // camera
    const camera = new THREE.PerspectiveCamera(45, (window.innerWidth - 20) / (window.innerHeight / 2), 0.1, 2000)
    camera.position.x = 12
    camera.position.y = 10
    camera.position.z = 10
    camera.lookAt(0, 0, 0)
    scene.add(camera)

    const camera2 = new THREE.PerspectiveCamera(10, (window.innerWidth - 20) / (window.innerHeight / 2), 0.1, 2000)
    camera2.position.x = 6
    camera2.position.y = 30
    camera2.position.z = -10
    camera2.lookAt(0, 0, 0)
    scene.add(camera2)

    // camera.fov = 46;
    // camera.zoom = 2.5;
    camera.updateProjectionMatrix()

    // loading files
    const loader = new FBXLoader()
    const gui = new dat.GUI({ autoPlace: false })

    // loader.load('files/body.FBX', obj => {
    //   obj.scale.x = obj.scale.y = obj.scale.z = 0.0005
    //   obj.position.x -= 15
    //   obj.traverse(function (child) {
    //     if (child.isMesh) {
    //       child.castShadow = true
    //       child.receiveShadow = true
    //     }
    //   })
    //   scene.add(obj)
    // })

    // loader.load('files/StaticMesh1.FBX', obj => {
    //   obj.scale.x = obj.scale.y = obj.scale.z = 0.5

    //   obj.position.x = 10
    //   obj.position.y = 0.5
    //   obj.position.z = 2.6

    //   obj.rotation.x = -90 * (Math.PI / 180)
    //   obj.rotation.z = -160 * (Math.PI / 180)

    //   scene.add(obj)
    // })

    // loader.load('files/StaticMesh2.FBX', obj => {
    //   // 3호기 집게 축
    //   obj.scale.x = obj.scale.y = obj.scale.z = 0.5

    //   obj.position.x = 6.7
    //   obj.position.y = -1.3
    //   obj.position.z = 2.8

    //   obj.rotation.x = -90 * (Math.PI / 180)
    //   obj.rotation.z = -10 * (Math.PI / 180)

    //   obj.traverse(function (child) {
    //     if (child.isMesh) {
    //       child.castShadow = true
    //       child.receiveShadow = true
    //     }
    //   })

    //   scene.add(obj)
    // })

    // loader.load('files/StaticMesh3.FBX', obj => {
    //   // 3호기 Y축
    //   obj.scale.x = obj.scale.y = obj.scale.z = 0.5

    //   obj.position.x = 5
    //   obj.position.z = 1.4

    //   obj.rotation.x = -90 * (Math.PI / 180)
    //   obj.rotation.z = -170 * (Math.PI / 180)

    //   obj.traverse(function (child) {
    //     if (child.isMesh) {
    //       child.castShadow = true
    //       child.receiveShadow = true
    //     }
    //   })

    //   scene.add(obj)
    // })

    // loader.load('files/StaticMesh4.FBX', obj => {
    //   // 3호기 몸체
    //   obj.scale.x = obj.scale.y = obj.scale.z = 0.5

    //   obj.position.x = 5

    //   obj.rotation.x = -90 * (Math.PI / 180)
    //   obj.rotation.z = -170 * (Math.PI / 180)

    //   obj.traverse(function (child) {
    //     if (child.isMesh) {
    //       child.castShadow = true
    //       child.receiveShadow = true
    //     }
    //   })

    //   scene.add(obj)
    // })

    const group = new THREE.Group()
    const group2 = new THREE.Group()

    // body
    // const StaticMesh = await loader.loadAsync('files/StaticMesh1.FBX')
    // group.add(StaticMesh)

    // loader 로 불러오면 3D 오브젝트 그대로 가져옴
    const StaticMesh1 = await loader.loadAsync('files/StaticMesh1.FBX')
    StaticMesh1.scale.x = StaticMesh1.scale.y = StaticMesh1.scale.z = 0.5
    StaticMesh1.position.x = 10
    StaticMesh1.position.y = 0.5
    StaticMesh1.position.z = 2.6
    StaticMesh1.rotation.x = -90 * (Math.PI / 180)
    StaticMesh1.rotation.z = -160 * (Math.PI / 180)

    const StaticMesh2 = await loader.loadAsync('files/StaticMesh2.FBX')
    StaticMesh2.scale.x = StaticMesh2.scale.y = StaticMesh2.scale.z = 0.5
    StaticMesh2.position.x = 6.7
    StaticMesh2.position.y = -1.3
    StaticMesh2.position.z = 2.8
    StaticMesh2.rotation.x = -90 * (Math.PI / 180)
    StaticMesh2.rotation.z = -10 * (Math.PI / 180)
    StaticMesh2.traverse(function (child) {
      if (child.isMesh) {
        child.castShadow = true
        child.receiveShadow = true
      }
    })

    const StaticMesh3 = await loader.loadAsync('files/StaticMesh3.FBX')
    // 3호기 Y축
    StaticMesh3.scale.x = StaticMesh3.scale.y = StaticMesh3.scale.z = 0.5
    StaticMesh3.position.x = 5
    StaticMesh3.position.z = 1.4
    StaticMesh3.rotation.x = -90 * (Math.PI / 180)
    StaticMesh3.rotation.z = -170 * (Math.PI / 180)
    StaticMesh3.traverse(function (child) {
      if (child.isMesh) {
        child.castShadow = true
        child.receiveShadow = true
      }
    })

    const StaticMesh4 = await loader.loadAsync('files/StaticMesh4.FBX')
    // 3호기 몸체
    StaticMesh4.scale.x = StaticMesh4.scale.y = StaticMesh4.scale.z = 0.5
    StaticMesh4.position.x = 5
    StaticMesh4.rotation.x = -90 * (Math.PI / 180)
    StaticMesh4.rotation.z = -170 * (Math.PI / 180)
    StaticMesh4.traverse(function (child) {
      if (child.isMesh) {
        child.castShadow = true
        child.receiveShadow = true
      }
    })
    group.add(StaticMesh1)
    group.add(StaticMesh2)
    group.add(StaticMesh3)
    group.add(StaticMesh4)

    // y 축 움직임
    group2.add(StaticMesh1)
    group2.add(StaticMesh2)
    group2.add(StaticMesh3)

    // x 축 움직임

    scene.add(group)
    scene.add(group2)

    const axisFolder = gui.addFolder('axis')
    axisFolder.add(group2.position, 'y', 0.5, 7, 0.1).name('위아래')

    // const groupObject = new THREE.Group()
    // groupObject.add(boxMesh)
    // groupObject.add(boxMesh2)
    // scene.add(groupObject)
    // groupObject.position.x = 10
    // axisFolder.add(groupObject.position, 'x', -10, 10, 0.2).name('X축')

    // axisFolder.add(groupObject.position, 'x', -10, 10, 0.2).name('X축')
    // axisFolder.add(groupObject.position, 'y', -10, 10, 0.2).name('Y축')
    // axisFolder.add(groupObject.position, 'z', -10, 10, 0.2).name('Z축')

    const renderer = new THREE.WebGLRenderer()
    renderer.setPixelRatio(window.devicePixelRatio)
    renderer.setSize(window.innerWidth - 20, window.innerHeight / 2)
    renderer.shadowMap.enabled = true
    // renderer.outputEncoding = THREE.sRGBEncoding;

    const container = document.querySelector('.container')
    container.appendChild(renderer.domElement)

    const stats = new Stats()
    document.body.appendChild(stats.dom)

    // gui controller

    container.appendChild(gui.domElement)
    gui.domElement.style.position = 'relative'
    gui.domElement.style.bottom = `${container.clientHeight - gui.domElement.clientHeight}px`
    gui.domElement.style.left = `${container.clientWidth - gui.domElement.clientWidth}px`
    // document.body.appendChild(gui.domElement) 이거는 container 밖에 있을 때
    container.appendChild(gui.domElement) // 컨테이너 안에서는 요롷게

    const light = new THREE.AmbientLight(0xffffff, 0.6)
    scene.add(light)

    const spotLight = new THREE.SpotLight(0xfd97e2, 0.3, 10, 10, 1, 1)
    spotLight.position.y = 10
    scene.add(spotLight)
    // scene.add(new THREE.SpotLightHelper(spotLight))

    // const material = new THREE.MeshStandardMaterial({ color: 'red' })
    // const material = new THREE.MeshPhongMaterial({ color: 'blue' })
    // const material2 = new THREE.MeshStandardMaterial({ color: 'red' })

    // box
    // const boxGeometry = new THREE.BoxGeometry(2, 2, 2)
    // const boxMesh = new THREE.Mesh(boxGeometry, material.clone())
    // boxMesh.position.z = -2
    // // scene.add(boxMesh) group 을 묶을 예정이기 때문에

    // const boxGeometry2 = new THREE.BoxGeometry(2, 2, 2)
    // const boxMesh2 = new THREE.Mesh(boxGeometry2, material.clone())
    // boxMesh2.position.z = 2
    // // scene.add(boxMesh2) group 을 묶을 예정이기 때문에

    // const boxGeometry3 = new THREE.BoxGeometry(2, 2, 2)
    // const boxMesh3 = new THREE.Mesh(boxGeometry3, material2.clone())
    // boxMesh3.position.z = -2

    // const boxGeometry4 = new THREE.BoxGeometry(2, 2, 2)
    // const boxMesh4 = new THREE.Mesh(boxGeometry4, material2.clone())
    // boxMesh4.position.z = 2

    // const groupObject = new THREE.Group()
    // groupObject.add(boxMesh)
    // groupObject.add(boxMesh2)
    // scene.add(groupObject)
    // groupObject.position.x = 10

    // const groupObject2 = new THREE.Group()
    // groupObject2.add(boxMesh3)
    // groupObject2.add(boxMesh4)
    // scene.add(groupObject2)
    // groupObject2.position.x = 11

    // 속도를 조절하기 위해서는 rendering 되는 변수도 같이 고려해주어야한다
    // const val = {
    //   speed: 0.01,
    //   speed2: 0.01
    // }

    // axisFolder.add(groupObject.position, 'x', -10, 10, 0.2).name('X축')
    // axisFolder.add(groupObject.position, 'y', -10, 10, 0.2).name('Y축')
    // axisFolder.add(groupObject.position, 'z', -10, 10, 0.2).name('Z축')

    // axisFolder.add(val, 'speed', 0.01, 0.05, 0.01).name('object1 속도')

    // axisFolder.add(groupObject2.position, 'x', -10, 10, 0.2).name('X축')
    // axisFolder.add(groupObject2.position, 'y', -10, 10, 0.2).name('Y축')
    // axisFolder.add(groupObject2.position, 'z', -10, 10, 0.2).name('Z축')

    // axisFolder.add(val, 'speed2', 0.01, 0.1, 0.01).name('object2 속도')

    // scene.add(group)

    // circle
    // const circleGeometry = new THREE.CircleGeometry(2, 30)
    // const circleMesh = new THREE.Mesh(circleGeometry, material.clone())
    // circleMesh.position.x = 4
    // scene.add(circleMesh)

    // scene.add(new THREE.AxesHelper(3))

    // cylinder
    // const cylinderGeometry = new THREE.CylinderGeometry(1, 1, 2, 24)
    // const cylinderMesh = new THREE.Mesh(cylinderGeometry, material.clone())
    // cylinderMesh.position.x = -4
    // scene.add(cylinderMesh)
    // scene.add(new THREE.BoxHelper(cylinderMesh))

    // sphere
    // const sphereGeometry = new THREE.SphereGeometry(1, 30, 30)
    // const sphereMesh = new THREE.Mesh(sphereGeometry, material.clone())
    // sphereMesh.position.z = 4
    // sphereMesh.position.y = 2
    // sphereMesh.layers.enable(1)
    // scene.add(sphereMesh)

    // sphereMesh.add(new THREE.AxesHelper(3))

    // grid
    // const gridHelper = new THREE.GridHelper(30, 30)
    // scene.add(gridHelper)

    // const gridHelper2 = new THREE.GridHelper(30, 30)
    // gridHelper2.rotateX(Math.PI / 2)
    // scene.add(gridHelper2)

    const control = new OrbitControls(camera, renderer.domElement)

    const raycaster = new THREE.Raycaster()
    raycaster.layers.set(1)
    const pointer = new THREE.Vector2()

    renderer.domElement.addEventListener('pointerdown', event => {
      const cx = event.clientX
      const cy = event.clientY
      const tx = event.offsetX
      const ty = event.offsetY

      const boundX = cx - tx
      const boundY = cy - ty

      const rx = cx - boundX
      const ry = cy - boundY

      const width = renderer.domElement.clientWidth
      const height = renderer.domElement.clientHeight

      const px = rx / width
      const py = ry / height

      const wX = px * 2 - 1
      const wY = -py * 2 + 1

      pointer.set(wX, wY)

      raycaster.setFromCamera(pointer, camera)
      const intersects = raycaster.intersectObjects(scene.children)

      if (intersects.length > 0) {
        const intersect = intersects[0]
        intersect.object.material.color.set(THREE.MathUtils.randInt(0x000000, 0xffffff))
      }
    })

    window.addEventListener('resize', () => {
      camera.aspect = (window.innerWidth - 20) / (window.innerHeight / 2)
      camera.updateProjectionMatrix()
      renderer.setSize(window.innerWidth - 20, window.innerHeight / 2)

      gui.domElement.style.bottom = `${container.clientHeight - gui.domElement.clientHeight}px`
      gui.domElement.style.left = `${container.clientWidth - gui.domElement.clientWidth}px`
    })

    // console.log(render)
    render()

    function render() {
      control.update()

      stats.update()

      // groupObject.rotation.x += val.speed
      // groupObject2.rotation.x += val.speed2

      // sphereMesh.rotation.x += val.speed

      renderer.render(scene, camera)
      requestAnimationFrame(render)
    }
  }
}
</script>
