---
title: 4th blog hehe
published_at: 2024-03-06
snippet: fractal art, Fractal art , FRACTAL ARTTT
disable_html_sanitization: true
---

# Hello, this is my fourth blog post. In this blog post I wanna go over my process of creating a fractal

## I am excited so I have this extra line but here we go

Tutorial from [https://www.youtube.com/watch?v=8JmoI4q7fTg&t=335s]

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
    //p1 will the top mid limit
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

This is my fractal tree and I learned how to make this from the blog as well as a video tutorial on YouTube. The video explained again what are the concept of recursion and why is it important to understand this concept in able to make fractals. Recursion is a function that can call itself, by calling itself multiple times. It’s like a Russian doll where the more you open it, the more the smaller version gets revealed. Like this fractal tree, the tree branches out to smaller branches and it keeps getting smaller and smaller until it reaches it limits. During the process of making this fractal tree. I documented the process of understanding through my code comments.

```
let p0 = {
        x: width / 2,
        y: height - 50
    };
    //p1 will the top mid limit
    let p1 = {
        x: width / 2,
        y: 50
    };
```

when making this tree, we have set out the height of the tree, p0 is the bottom and p1 is the top of the tree. And then from there, we can create the branches of the tree. Call the three branches pA, pB and pC.

```
pA = {
x: p0.x + dx _ trunkRatio,
y: p0.y + dy _ trunkRatio
},
pB = {
x: pA.x + Math.cos(angle + branchAngle) _ branchLength,
y: pA.y + Math.sin(angle + branchAngle) _ branchLength
},
pC = {
x: pA.x + Math.cos(angle - branchAngle) _ branchLength,
y: pA.y + Math.sin(angle - branchAngle) _ branchLength
};
```

Then here I created a recursive function to make the tree branches and for them to expand and call itself within the limit that we have set

```
function tree(p0, p1, limit) {
let dx = p1.x - p0.x,
dy = p1.y - p0.y,
dist = Math.sqrt(dx _ dx + dy _ dy),
angle = Math.atan2(dy, dx),
branchLength = dist \* (1 - trunkRatio),
```

This is the limit setting for the branches, using boolean logic, to set out the the limit and create recursion so that the tree branches. If the setting fit in with the else condition, then the code will draw out new branches at pB and pC.

```
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
```

This is my fractal tree and I learned how to make this from the blog as well as a video tutorial on YouTube. The video explained again what are the concept of recursion and why is it important to understand this concept in able to make fractals. Recursion is a function that can call itself, by calling itself multiple times. It’s like a Russian doll where the more you open it, the more the smaller version gets revealed. Like this fractal tree, the tree branches out to smaller branches and it keeps getting smaller and smaller until it reaches it limits. During the process of making this fractal tree. I documented the process of understanding through my code comments.

let p0 = {
x: width / 2,
y: height - 50
};
//p1 will the top mid limit
let p1 = {
x: width / 2,
y: 50
};
when making this tree, we have set out the height of the tree, p0 is the bottom and p1 is the top of the tree. And then from there, we can create the branches of the tree. Call the three branches pA, pB and pC.
pA = {
x: p0.x + dx _ trunkRatio,
y: p0.y + dy _ trunkRatio
},
pB = {
x: pA.x + Math.cos(angle + branchAngle) _ branchLength,
y: pA.y + Math.sin(angle + branchAngle) _ branchLength
},
pC = {
x: pA.x + Math.cos(angle - branchAngle) _ branchLength,
y: pA.y + Math.sin(angle - branchAngle) _ branchLength
};

Then here I created a recursive function to make the tree branches and for them to expand and call itself within the limit that we have set
function tree(p0, p1, limit) {
let dx = p1.x - p0.x,
dy = p1.y - p0.y,
dist = Math.sqrt(dx _ dx + dy _ dy),
angle = Math.atan2(dy, dx),
branchLength = dist \* (1 - trunkRatio),

This is the limit setting for the branches, using boolean logic, to set out the the limit and create recursion so that the tree branches. If the setting fit in with the else condition, then the code will draw out new branches at pB and pC.
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

Those are the three most essential codes that conduct and set out the limit for the recursive function. Mistakes were made as I kept getting errors but it was a human error with me forgetting comas and forgot to close my script tag. Other than that, it was a straightforward process.

This process if expanded to more branches could be a perfect example of chaos with more complex shapes and branches and I could potentially expanded it for my assignment 2. Another form of recursive function like Barnsley ferns could be used to explain the concept of chaos
