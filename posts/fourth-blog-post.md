---
title: 4th blog hehe
published_at: 2024-03-06
snippet: fractal art, Fractal art , FRACTAL ARTTT
disable_html_sanitization: true
---

# Hello, this is my fourth blog post. In this blog post I wanna go over my process of creating a fractal

## I am excited so I have this extra line but here we go

<canvas id="canvas"></canvas>

<script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    // Function to draw the tree
    function drawTree(x, y, length, angle, depth) {
        if (depth === 0) return;

        const x1 = x + length * Math.cos(angle);
        const y1 = y + length * Math.sin(angle);

        ctx.beginPath();
        ctx.moveTo(x, y);
        ctx.lineTo(x1, y1);
        ctx.strokeStyle = 'white';
        ctx.lineWidth = depth;
        ctx.stroke();

        drawTree(x1, y1, length * 0.8, angle - Math.PI / 6, depth - 1);
        drawTree(x1, y1, length * 0.8, angle + Math.PI / 6, depth - 1);
    }

    // Initial call to draw the tree
    drawTree(canvas.width / 2, canvas.height, 120, -Math.PI / 2, 12);
</script>
