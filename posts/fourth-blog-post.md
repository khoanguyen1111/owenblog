---
title: 4th blog hehe
published_at: 2024-03-06
snippet: fractal art, Fractal art , FRACTAL ARTTT
disable_html_sanitization: true
---

# Hello, this is my fourth blog post. In this blog post I wanna go over my process of creating a fractal

## I am excited so I have this extra line but here we go

<canvas id='fractal_tree'></canvas>

<script type='module'>

    // get and format canvas
    const cnv = document.getElementById('fractal_tree');
    const width = cnv.parentNode.scrollWidth;
    const height = width * 9 / 16;
    cnv.width = width;
    cnv.height = height;

    // get canvas context
    const ctx = cnv.getContext('2d');

    let p0 = {
        x: width / 2,
        y: height - 50
    };
    let p1 = {
        x: width / 2,
        y: 50
    };
    let branchAngle = Math.PI / 4;
    let trunkRatio = 0.5;

    
    tree(p0, p1, 15);

    function tree(p0, p1, limit) {
        let dx = p1.x - p0.x,
            dy = p1.y - p0.y,
            dist = Math.sqrt(dx * dx + dy * dy),
            angle = Math.atan2(dy, dx),
            branchLength = dist * (1 - trunkRatio),
            pA = {
                x: p0.x + dx * trunkRatio,
                y: p0.y + dy * trunkRatio
            },
            pB = {
                x: pA.x + Math.cos(angle + branchAngle) * branchLength,
                y: pA.y + Math.sin(angle + branchAngle) * branchLength
            },
            pC = {
                x: pA.x + Math.cos(angle - branchAngle) * branchLength,
                y: pA.y + Math.sin(angle - branchAngle) * branchLength
            };

        ctx.beginPath();
        ctx.moveTo(p0.x, p0.y);
        ctx.lineTo(pA.x, pA.y);
        ctx.stroke();

        if (limit > 0) {
            tree(pA, pC, limit - 1);
            tree(pA, pB, limit - 1);
        } else {
            ctx.beginPath();
            ctx.moveTo(pB.x, pB.y);
            ctx.lineTo(pA.x, pA.y);
            ctx.lineTo(pC.x, pC.y);
            ctx.stroke();
        }
    }
</script>

```
<canvas id='fractal_tree'></canvas>

<script type='module'>

    // get and format canvas
    const cnv = document.getElementById('fractal_tree');
    const width = cnv.parentNode.scrollWidth;
    const height = width * 9 / 16;
    cnv.width = width;
    cnv.height = height;

    // get canvas context
    const ctx = cnv.getContext('2d');

    //creating point of limits
    //p0 is the bottom mid limit
    let p0 = {
        x: width / 2,
        y: height - 50
    };
    //p1 will the top mid limmit
    let p1 = {
        x: width / 2,
        y: 50
    };
    // this is the branch angle, i choose angle of 45 degree
    // hence its Math.PI/4
    let branchAngle = Math.PI / 4;
    let trunkRatio = 0.5;

    // this is the amount of branches the tree will have
    tree(p0, p1, 15);
    //// this is the start of recursive tree function
    function tree(p0, p1, limit) {
        let dx = p1.x - p0.x,
            dy = p1.y - p0.y,
            dist = Math.sqrt(dx * dx + dy * dy),
            angle = Math.atan2(dy, dx),
            branchLength = dist * (1 - trunkRatio),
            pA = {
                x: p0.x + dx * trunkRatio,
                y: p0.y + dy * trunkRatio
            },
            pB = {
                x: pA.x + Math.cos(angle + branchAngle) * branchLength,
                y: pA.y + Math.sin(angle + branchAngle) * branchLength
            },
            pC = {
                x: pA.x + Math.cos(angle - branchAngle) * branchLength,
                y: pA.y + Math.sin(angle - branchAngle) * branchLength
            };

        // begin draw path
        ctx.beginPath();
        ctx.moveTo(p0.x, p0.y);
        ctx.lineTo(pA.x, pA.y);
        ctx.stroke();

        // limit setting for the branches
        if (limit > 0) {
            tree(pA, pC, limit - 1);
            tree(pA, pB, limit - 1);
        } else { // reached these limit and draw out branches
            ctx.beginPath();
            ctx.moveTo(pB.x, pB.y);
            ctx.lineTo(pA.x, pA.y);
            ctx.lineTo(pC.x, pC.y);
            ctx.stroke();
        }
    }
</script>
```
