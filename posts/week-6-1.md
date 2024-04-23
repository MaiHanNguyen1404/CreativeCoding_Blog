---
title: Week 6.1 Blog
published_at: 2024-04-23
snippet: Week 6 Homework - Three.js
disable_html_sanitization: true
---

<div id="three_container"></div>

<script id="three_script" type="module"> 
   import * as THREE from "/scripts/three/three.module.js"
   import { OrbitControls } from "/scripts/three/OrbitControls.js"
   
   const div = document.getElementById ("three_container")

   const width = div.parentNode.scrollWidth
   const height = width * 9 / 16

   //  Instanced Buffer Geomety
   // from https://codepen.io/prisoner849/pen/REyzJV
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(60, 1, 1, 1000);
    camera.position.set(0, 0, 5);
    var renderer = new THREE.WebGLRenderer({
    antialias: true
    });
    renderer.setClearColor(0x808080);
    var canvas = renderer.domElement;
    document.body.appendChild(canvas);

    var controls = new THREE.OrbitControls(camera, canvas);

    // texture
    var tCanvas = document.createElement("canvas");
    tCanvas.width = 128;
    tCanvas.height = 128;
    var tCtx = tCanvas.getContext('2d');
    tCtx.clearRect(0, 0, tCanvas.width, tCanvas.height);

    var texture = new THREE.CanvasTexture(tCanvas);
    //var texture = new THREE.TextureLoader().load('https://threejs.org/examples/textures/UV_Grid_Sm.jpg');
    var lineColor = new THREE.Color();
    function drawSomething(){
    tCtx.beginPath();
    tCtx.moveTo(THREE.Math.randInt(0, 127), THREE.Math.randInt(0, 127));
    tCtx.lineTo(THREE.Math.randInt(0, 127), THREE.Math.randInt(0, 127));
    tCtx.lineWidth = THREE.Math.randInt(5, 20);
    lineColor.set(Math.random() * 0x808080 + 0x808080);
    tCtx.strokeStyle = lineColor.getStyle();
    tCtx.stroke();
    texture.needsUpdate = true;
    }

    setInterval( drawSomething, 500 );

    var planeGeom = new THREE.PlaneBufferGeometry(2, 2);

    var instancedGeom = new THREE.InstancedBufferGeometry();
    instancedGeom.attributes.position = planeGeom.attributes.position;
    instancedGeom.attributes.uv = planeGeom.attributes.uv;
    instancedGeom.index = planeGeom.index;

    instancedGeom.addAttribute("instancePosition", new THREE.InstancedBufferAttribute( new Float32Array([-1.1, 1.1, 0, 1.1, 1.1, 0, -1.1, -1.1, 0, 1.1, -1.1, 0]), 3));
    instancedGeom.addAttribute("instanceUv", new THREE.InstancedBufferAttribute(new Float32Array([0, 1, 1, 1, 0, 0, 1, 0]), 2));

    var material = new THREE.ShaderMaterial({
    uniforms: {
        texture1: { value: texture},
        textureDivision: {value: new THREE.Vector2(2, 2)},
        time: {value: 0}
    },
    vertexShader:`
        precision highp float;

        uniform vec2 textureDivision;
        uniform float time;

            attribute vec3 instancePosition;
            attribute vec2 instanceUv;
        
            varying vec2 vUv;

            void main(){
        vec2 slices = vec2(1.0) / textureDivision;
                vUv = slices * instanceUv + slices * uv;
        vec3 pos = position + instancePosition;
        pos += normalize(instancePosition) * (sin(time) * 0.5 + 0.5);
        
                gl_Position = projectionMatrix * modelViewMatrix * vec4( pos, 1.0 );
            }
    `,
    fragmentShader:`
        precision highp float;

        uniform sampler2D texture1;
        
            varying vec2 vUv;

            void main() {
                gl_FragColor = texture2D(texture1, vUv);
            }
    `
    });

    var instancedMesh = new THREE.Mesh(instancedGeom, material);
    scene.add(instancedMesh);

    scene.add(new THREE.AxesHelper(0.1));


    render();

    function render() {
    if (resize(renderer)) {
        camera.aspect = canvas.clientWidth / canvas.clientHeight;
        camera.updateProjectionMatrix();
    }
    material.uniforms.time.value = performance.now() / 1000;
    renderer.render(scene, camera);
    requestAnimationFrame(render);
    }

    function resize(renderer) {
    const canvas = renderer.domElement;
    const width = canvas.clientWidth;
    const height = canvas.clientHeight;
    const needResize = canvas.width !== width || canvas.height !== height;
    if (needResize) {
        renderer.setSize(width, height, false);
    }
    return needResize;
    }


</script>

