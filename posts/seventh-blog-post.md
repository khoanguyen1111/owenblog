---
title: 7th blog hehe
published_at: 2024-03-06
snippet: Combining other elements with Ascii cam
disable_html_sanitization: true
---

<script src="/script/c2.js"></script>

<canvas id="c2"></canvas>

<div id="ascii_div"></div>

<script>
const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Line {
    constructor() {
        let x1 = random.next(renderer.width);
        let y1 = random.next(renderer.height);
        let x2 = random.next(renderer.width);
        let y2 = random.next(renderer.height);
        super(x1, y1, x2, y2);

        this.v1 = new c2.Vector(random.next(-5, 5), random.next(-5, 5));
        this.v2 = new c2.Vector(random.next(-5, 5), random.next(-5, 5));
        this.weight = random.next(1, 5);
        this.color = c2.Color.hsl(random.next(0, 30), random.next(30, 60), random.next(20, 100));
    }

    update(){
        this.bounce(this.p1, this.v1);
        this.bounce(this.p2, this.v2);
    }

    bounce(p, v){
        p.x += v.x;
        p.y += v.y;

        if (p.x < 0) {
            p.x = 0;
            v.x *= -1;
        } else if (p.x > renderer.width) {
            p.x = renderer.width;
            v.x *= -1;
        }
        if (p.y < 0) {
            p.y = 0;
            v.y *= -1;
        } else if (p.y > renderer.height) {
            p.y = renderer.height;
            v.y *= -1;
        }
    }
}

let agents = [];
for (let i = 0; i < 15; i++) agents[i] = new Agent();

 const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"

   const div = document.getElementById (`ascii_div`)
   div.style.fontFamily = `monospace`
   div.style.textAlign = `center`

   renderer.draw (() => {
      renderer.clear ()

      let delaunay = new c2.Delaunay ()
      delaunay.compute (agents)
      let vertices = delaunay.vertices
      let edges = delaunay.edges
      let triangles = delaunay.triangles

      let maxArea = 0
      let minArea = Number.POSITIVE_INFINITY;
      for (let i = 0; i < triangles.length; i++) {
         let area = triangles[i].area ()
         if (area < minArea) minArea = area
         if (area > maxArea) maxArea = area
      }

      renderer.stroke (false)
      for (let i = 0; i < triangles.length; i++) {
         let t = c2.norm (triangles[i].area(), minArea, maxArea)
         let color = c2.Color.hsl (315+30*t, 30+30*t, 20+80*t)
         renderer.fill (color)
         renderer.triangle (triangles[i])
      }

      for (let i = 0; i < agents.length; i++) {
         agents[i].update ()
      }
      
      const w = renderer.canvas.width
      const h = renderer.canvas.height
      const pixels = renderer.context.getImageData (0, 0, w, h).data

      let ascii_img = ``

      for (let y = 0; y < renderer.canvas.height; y += 22) {
         for (let x = 0; x < renderer.canvas.width; x += 10) {
            const i = (y * renderer.canvas.width + x) * 4
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]
            const br = (r * g * b / 16581376) ** 0.1
            const char_i = Math.floor (br * chars.length)
            ascii_img += chars[char_i]
         }
         ascii_img += `\n`
      }

      div.innerText = ascii_img

   })

   function resize () {
      let parent = renderer.canvas.parentElement
      renderer.size (parent.clientWidth, parent.clientWidth / 16 * 9)
   }
</script>
