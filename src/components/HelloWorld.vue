<template>
  <canvas :width=windowWidth :height=windowHeight ref="ccontain"/>
</template>

<script>
import * as THREE from 'three'
export default {
  name: 'HelloWorld',
  data () {
    return {
      windowWidth: window.innerWidth,
      windowHeight: window.innerHeight
    }
  },
  methods: {
    windowResize: function () {
      this.windowWidth = window.innerWidth
      this.windowHeight = window.innerHeight
    }
  },
  mounted: function () {
    window.addEventListener('resize', this.windowResize)
    var scene = new THREE.Scene()
    var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)

    var renderer = new THREE.WebGLRenderer({
      canvas: this.$refs.ccontain
    })
    var geometry = new THREE.BoxGeometry(1, 1, 1)
    var material = new THREE.MeshBasicMaterial({ color: 0x00ff00 })
    var cube = new THREE.Mesh(geometry, material)
    scene.add(cube)

    camera.position.z = 5

    var animate = function () {
      requestAnimationFrame(animate)
      cube.rotation.x += 0.1
      cube.rotation.y += 0.1
      renderer.render(scene, camera)
    }

    animate()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
