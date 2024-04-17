---
title: Adding c2.js
published_at: 2024-03-29
snippet: Sixth week demo in class
disable_html_sanitization: true
---

## This is a in class demo blog

<script src="../script/c2.js"></script>;
<!-- <script src="static/p5/p5.js"></script>; -->

<canvas id='c2'/>

<script>
console.log ('hi')
// by Ren Yuan

const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();

class Agent extends c2.Point {
constructor() {
let x = random.next(renderer.width);
let y = random.next(renderer.height);
super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        renderer.stroke('#333333');
        renderer.lineWidth(5);
        renderer.point(this.x, this.y);
    }

}

let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();

renderer.draw(() => {
renderer.clear();

    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }


    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }

});

window.addEventListener('resize', resize);
function resize() {
let parent = renderer.canvas.parentElement;
renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}




</script>

<script>
//Created by Ren Yuan


const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Circle{
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        let r = random.next(renderer.width/4);
        super(x, y, r);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
        this.color = c2.Color.hsl(random.next(0, 30), random.next(30, 60), random.next(20, 100));
    }

    update(){
        this.p.x += this.vx;
        this.p.y += this.vy;

        if (this.p.x < this.r) {
            this.p.x = this.r;
            this.vx *= -1;
        } else if (this.p.x > renderer.width-this.r) {
            this.p.x = renderer.width-this.r;
            this.vx *= -1;
        }
        if (this.p.y < this.r) {
            this.p.y = this.r;
            this.vy *= -1;
        } else if (this.p.y > renderer.height-this.r) {
            this.p.y = renderer.height-this.r;
            this.vy *= -1;
        }
    }

    display(){
        renderer.stroke(false);
        renderer.fill(this.color);
        renderer.circle(this);
    }
}


let agents = [];
for (let i = 0; i < 10; i++) agents[i] = new Agent();


renderer.draw(() => {
    renderer.clear();

    for (let i = 0; i < agents.length; i++) {
        agents[i].update();
        agents[i].display();
    }

    for (let i = 0; i < agents.length-1; i++) {
        for (let j = i+1; j < agents.length; j++) {
          let points = agents[i].intersection(agents[j]);
            if(points!=null){
              let c = c2.Color.lerp(agents[i].color, agents[j].color, .5);
              renderer.stroke(c);
              renderer.lineWidth(2);
              renderer.line(points[0].x, points[0].y, points[1].x, points[1].y);
              
              renderer.stroke('#333333');
              renderer.lineWidth(5);
              renderer.point(points[0]);
              renderer.point(points[1]);
            }
        }
    }
});


window.addEventListener('resize', resize);
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>
