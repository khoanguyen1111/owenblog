---
title: 6th blog hehe part2
published_at: 2024-03-06
snippet: The C2 and Threejs experimentation
disable_html_sanitization: true
---

<canvas id="cnv" width="800" height="800"></canvas>

<div class="writing unselectable" id="idWire">Wire Boxes</div>
<div class="writing unselectable" id="idRev">Rev0.1</div>
<script async src="https://ga.jspm.io/npm:es-module-shims@1.5.1/dist/es-module-shims.js" crossorigin="anonymous"></script>

<script type = "module">
import {Scene, PerspectiveCamera, Vector2, Vector3, Object3D, MathUtils} from "/script/three/three.js";
import {OrbitControls} from "/script/three/OrbitControls.js";
console.clear();

class WireSegments extends Object3D {
  constructor(points, index){
    super();
    this.points = points;
    this.index = index;
    this.linePoints = new Array(2).fill().map(_ => {return new Vector3()});
    this.color = "maroon";
    this.lineWidth = 2;
    this.isWireSegments = true;
  }
}

class WireRenderer{
  constructor(cnv, ctx){
    this.canvas = cnv;
    this.context = ctx;
    this.size = new Vector3();
  }
  render(scene, camera){
    scene.updateMatrixWorld();
    camera.updateMatrixWorld();
    this.size.set(this.canvas.width * 0.5, this.canvas.height * 0.5, 1);
    let c = this.context;
    scene.traverse(object => {
      if (object.isWireSegments){
        c.save();
        c.strokeStyle = object.color;
        c.lineWidth = object.lineWidth;
        c.beginPath();
        object.index.forEach(idx => {
          object.linePoints.forEach((lp, lpIdx) => {
            lp.copy(object.points[idx[lpIdx]]);
            object.localToWorld(lp);  
            lp.project(camera);
            lp.y *= -1; 
            lp.multiply(this.size).add(this.size);
          })
          c.moveTo(object.linePoints[0].x, object.linePoints[0].y);
          c.lineTo(object.linePoints[1].x, object.linePoints[1].y);
        })
        c.stroke();
        c.restore();
      }
    })
  }
}

let ctx = cnv.getContext("2d");

let scene = new Scene();
let camera = new PerspectiveCamera(60, 1, 1, 100);
camera.position.setFromSphericalCoords(30, Math.PI / 3, Math.PI * 4 / 5);
let renderer = new WireRenderer(cnv, ctx);
let controls = new OrbitControls(camera, cnv);
controls.minDistance = 15;
controls.maxDistance = 30;
controls.enableDamping = true;
controls.enablePan = false;

let v3 = new Vector3();
let linePoints = [];
let lineIndex = [];
for(let i = 0; i < 25; i++){
  let axisSize = 15;
  let axisRnd = MathUtils.randInt(0, 2);
  v3.random().subScalar(0.5).multiplyScalar(axisSize);
  linePoints.push(
    v3.clone().setComponent(axisRnd, -axisSize), 
    v3.clone().setComponent(axisRnd, axisSize)
  );
  lineIndex.push([i * 2 + 0, i * 2 + 1]);
  let line = new WireSegments(linePoints, lineIndex);
  line.color = "black";
  line.lineWidth = 0.05;
  scene.add(line);
}


let boxes = [];
let unit = 0.5;
let dims = {x: 1, y: 1, z: 1};
let points = [
  [-unit, unit, -unit],[unit, unit, -unit],[unit, -unit, -unit],[-unit, -unit, -unit],
  [-unit, unit, unit],[unit, unit, unit],[unit, -unit, unit],[-unit, -unit, unit]
].map( p => {return new Vector3(p[0] * dims.x, p[1] * dims.y, p[2] * dims.z)});
let index = [
  [0, 1], [1, 2], [2, 3], [3, 0],
  [0, 4], [1, 5], [2, 6], [3, 7],
  [4, 5], [5, 6], [6, 7], [7, 4]
];
for(let i = 0; i < 50; i++){
  let box = new WireSegments(points, index);
  box.position.random().subScalar(0.5).multiplyScalar(15);
  box.scale.setScalar(MathUtils.randInt(2, 5));
  box.userData = {
    prevTime: 0,
    widthPhase: Math.PI * 2 * Math.random()
  }
  scene.add(box);
  boxes.push(box);
}

let timeStart = performance.now();

draw();
function draw(){
  let t = (performance.now() - timeStart) * 0.001;
  controls.update();
  
  ctx.clearRect(0, 0, cnv.width, cnv.height);
  
  let boxTime = t * 0.5;
  
  ctx.lineCap = "round";
  
  boxes.forEach(box => {
    
    let currTime = (box.userData.widthPhase + boxTime * Math.PI) % (Math.PI * 2);
    if (currTime < box.userData.prevTime) {
      box.position.random().subScalar(0.5).multiplyScalar(15);
      box.scale.setScalar(MathUtils.randInt(2, 5));
    }
    
    let sinVal = Math.sin(currTime - Math.PI * 0.5) * 0.5 + 0.5;
    box.lineWidth = sinVal * 4;
    
    box.userData.prevTime = currTime;
  }) 
  
  renderer.render(scene, camera);
  requestAnimationFrame(draw);
}

</script>
