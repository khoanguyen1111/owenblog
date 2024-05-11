---
title: Assignment 2 Blog
published_at: 2024-03-30
snippet: Assignment 2 recap and understanding
disable_html_sanitization: true
---

<canvas id="tv_glitch"></canvas>

<script type="module">
    const cnv = document.getElementById('tv_glitch');
    const ctx = cnv.getContext('2d');

    // Size the canvas to fit its parent container
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;

    // Background color
    cnv.style.backgroundColor = 'darkseagreen';

    let hitMe = true; // Boolean variable to control animation

    // Function to generate random noise with color
    function generateRandomColoredNoise(width, height) {
        const noiseData = ctx.createImageData(width, height);
        for (let i = 0; i < noiseData.data.length; i += 4) {
            // Generate random values for RGB channels
            const red = Math.floor(Math.random() * 256);
            const green = Math.floor(Math.random() * 256);
            const blue = Math.floor(Math.random() * 256);
            // Assign random color to each pixel
            noiseData.data[i] = red; // Red channel
            noiseData.data[i + 1] = green; // Green channel
            noiseData.data[i + 2] = blue; // Blue channel
            noiseData.data[i + 3] = 255; // Alpha channel
        }
        return noiseData;
    }

    // Function to apply glitch effect to the canvas
    function applyGlitchEffect() {
        // Generate random colored noise
        const noiseData = generateRandomColoredNoise(cnv.width, cnv.height);
        // Draw the noise pattern on the canvas
        ctx.putImageData(noiseData, 0, 0);
    }

    // Class for bouncing text
    class BouncingText {
        constructor(x, y, text, fontSize) {
            this.x = x;
            this.y = y;
            this.text = text;
            this.dx = Math.random() * 2 + 1; // Speed in x direction
            this.dy = Math.random() * 2 + 1; // Speed in y direction
            this.color = `rgb(${Math.random() * 255},${Math.random() * 255},${Math.random() * 255})`; // Random color
            this.fontSize = fontSize; // Font size
        }

        update() {
            // Bounce off horizontal borders
            if (this.x < 0 || this.x + ctx.measureText(this.text).width > cnv.width) {
                this.dx *= -1;
            }
            // Bounce off vertical borders
            if (this.y < this.fontSize || this.y + this.fontSize > cnv.height) {
                this.dy *= -1;
            }
            // Update position
            this.x += this.dx;
            this.y += this.dy;
        }

        draw() {
            ctx.fillStyle = this.color;
            ctx.font = `${this.fontSize}px Arial`; // Set font size
            ctx.fillText(this.text, this.x, this.y);
        }
    }

    // Array to hold bouncing text objects
    const textArr = [];

    // Function to create bouncing texts
    function createBouncingTexts() {
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 50)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 60)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "YOU", 20)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "I", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "LOVE", 70)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "YOU", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 80)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 40)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "YOU", 70)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "I", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "LOVE", 50)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "YOU", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 70)); // Add bouncing text
         textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "PRESS", 90)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "SPACE", 90)); // Add bouncing text
        // Add more bouncing texts as needed
    }

    // Function to update and draw bouncing texts
    function updateAndDrawBouncingTexts() {
        // Apply glitch effect if animation is toggled on
        if (hitMe) {
            applyGlitchEffect();
        }
        // Update and draw each bouncing text if animation is toggled on
        if (hitMe) {
            textArr.forEach(text => {
                text.update();
                text.draw();
            });
        }
    }

    // Function to create glitch effect animation
    function glitchAnimation() {
        // Clear canvas
        ctx.clearRect(0, 0, cnv.width, cnv.height);
        // Update and draw bouncing texts
        updateAndDrawBouncingTexts();
        // Schedule next frame
        if (hitMe) {
            requestAnimationFrame(glitchAnimation);
        }
    }

    // Start the glitch animation
    createBouncingTexts(); // Create initial bouncing texts
    glitchAnimation();

    // Toggle animation on spacebar press
    document.addEventListener('keydown', function(event) {
        if (event.code === 'Space') {
            hitMe = !hitMe; // Toggle animation
            if (hitMe) {
                glitchAnimation(); // Start animation if toggled on
            }
        }
    });
</script>

# Hey what a long code, I know... so let's break it down

Let's start with how I came up with this:
Step 1: Deciding what do I want to do:
I was thinking of doing an expansion of my refractal tree and create a bigger and more impressive tree.However, I came back to look at some of artist that were given as inspiration for this project, I was really interested with Sabato Visconti's art. I don't know why but the concept of "glitch-ness" fascinated me. When talking about chaotic, glitches for me is what create that chaos, it distorts the orginal piece, bring a new persepctive to the art piece. Taking step further to have a conversation about effective complexity a bit, is about finding the balance or equilibrium of chaotic and order. Eventhough glitch is to say when an image is acting weird with flashes of RGB on the picture, however it does not ruin the complete picture but instead it remixes the picture. Just like how some people like another remix version of song even though it is completely different from the original song. From there, I want to start dig deeper and find more about her art piece and I started to developed my code

Step 2: Setting up the baseline of the code
So, now I have the idea, I want to start doing the coding bit, I was not ready for this by the way, I start to find some more resources that similar to my idea. I have the baseline which are the code from week 5 class. However, I want to make a glitch without an image. I want to have this ambience of an old TV that when there no chanel working, so that is where I want to start with. As a first time coder, I have ideas but abilities are limiting behind so I went to ask for tutorial. There are no particular one that I can learn that are close to what I wanted to do so I went and salvage what I have done for the glitch homework. After that I feel a bit lost and since none of the code tutorial really do what I want, I asked ChatGPT for help. It provides me with essential help that I couldn't find anywhere on the internet. Now that I gather the baseline, the idea, lets start coding.

Step 3: Break it down...

start wiith the basic shall wee

```<canvas id="tv_glitch"></canvas>

<script type="module">
    const cnv = document.getElementById('tv_glitch');
    const ctx = cnv.getContext('2d');

    // Size the canvas to fit its parent container
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;

    // Background color
    cnv.style.backgroundColor = 'darkseagreen';
```

basically, create a canvas and set a background color, basic stuff that we have been doing in class with the canvas API

```
 // Function to generate random noise with color
    function generateRandomColoredNoise(width, height) {
        const noiseData = ctx.createImageData(width, height);
        for (let i = 0; i < noiseData.data.length; i += 4) {
            // Generate random values for RGB channels
            const red = Math.floor(Math.random() * 256);
            const green = Math.floor(Math.random() * 256);
            const blue = Math.floor(Math.random() * 256);
            // Assign random color to each pixel
            noiseData.data[i] = red; // Red channel
            noiseData.data[i + 1] = green; // Green channel
            noiseData.data[i + 2] = blue; // Blue channel
            noiseData.data[i + 3] = 255; // Alpha channel
        }
        return noiseData;
    }
```

here we get to the good stuff so let's see it. First of all to be able to create that noise background you see behind, a function called generatedRandomColoredNoise is needed to achieve the effects. It created that noisy background with random color, it is RGB, to have that background. Next we talk about the for loop that repeat the glicth pixel over and over again. Then we move to the constant RGB color with random value so that the color will appear randomly.

```
 // Function to apply glitch effect to the canvas
    function applyGlitchEffect()
        // Generate random colored noise
        const noiseData = generateRandomColoredNoise(cnv.width, cnv.height);
        // Draw the noise pattern on the canvas
        ctx.putImageData(noiseData, 0, 0);
```

UP NEXXTTT, we have the function call applyGlitchEffect, like the name said, it applied glitch effect to the function, with the noise pattern we generated up there. When I called this function, is when the glitch started glitching, create that noise you see at the background. So now I have a glitchy background that act like a noisy broken TV screen. Well I said that is boring so I added something. Looked back at Sabato Visconti's art, it had a lot of text and object floating around, so I said, cool, let's do that. I added text, but with a COOL TWSIT

```
 class BouncingText {
        constructor(x, y, text, fontSize) {
            this.x = x;
            this.y = y;
            this.text = text;
            this.dx = Math.random() * 2 + 1; // Speed in x direction
            this.dy = Math.random() * 2 + 1; // Speed in y direction
            this.color = `rgb(${Math.random() * 255},${Math.random() * 255},${Math.random() * 255})`; // Random color
            this.fontSize = fontSize; // Font size
        }
 }
```

BOUNCE TEXT, cool right, i don't know. So I added text but it bounce it of the wall of the canvas. Let's break it down shall we. First, I created a class called bouncing text with the constructor inside which direct the speed of the text when travelling within the canvas with a safe speed. The speed is between 1 and 3. Changing it causing the speed of the text to go all crazy and hard to see

````
  update() {
            // Bounce off horizontal borders
            if (this.x < 0 || this.x + ctx.measureText(this.text).width > cnv.width) {
                this.dx *= -1;
            }
            // Bounce off vertical borders
            if (this.y < this.fontSize || this.y + this.fontSize > cnv.height) {
                this.dy *= -1;
            }
            // Update position
            this.x += this.dx;
            this.y += this.dy;
        }

    ```
Right here we have the reason for its to bounce and goes all crazy. We set a condition for it to bounces off the two side, which are x and y of the canvas. For x, y we set a condition so that it must commit to the else, which are if this x is less then 0 and the x position passes the canvas width, then it will bounce off. For y , if the position went passed the canvas top and bottom, it will bounce off.
````

const textArr = [];

    // Function to create bouncing texts
    function createBouncingTexts() {
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 50)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 60)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "YOU", 20)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "I", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "LOVE", 70)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "YOU", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 80)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 40)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "LOVE", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "YOU", 70)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "I", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "LOVE", 50)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "YOU", 30)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "I", 70)); // Add bouncing text
         textArr.push(new BouncingText(cnv.width / 3, cnv.height / 3, "PRESS", 90)); // Add bouncing text
        textArr.push(new BouncingText(cnv.width / 2, cnv.height / 2, "SPACE", 90)); // Add bouncing text
        // Add more bouncing texts as needed
    }
    ```

From here we make the text array to create the floating text, you know, to have actual words,... Anyway, I put a bunch of I LOVE YOU text because I am feel like the word I love you is so pure from a kid to an old man and it carries such meaning to it that in this chaotic world, that sentence keep the world together. Also, Press Space, I gonna explain it later but for now this is this.
I remember last assignment I missed out by not doing boolean logic, this time I remembered, so I added this

```
 let hitMe = true; // Boolean variable to control animation
```

    function glitchAnimation() {
        // Clear canvas
        ctx.clearRect(0, 0, cnv.width, cnv.height);
        // Update and draw bouncing texts
        updateAndDrawBouncingTexts();
        // Schedule next frame
        if (hitMe) {
            requestAnimationFrame(glitchAnimation);
        }
    }

    // Start the glitch animation
    createBouncingTexts(); // Create initial bouncing texts
    glitchAnimation();

    // Toggle animation on spacebar press
    document.addEventListener('keydown', function(event) {
        if (event.code === 'Space') {
            hitMe = !hitMe; // Toggle animation
            if (hitMe) {
                glitchAnimation(); // Start animation if toggled on
            }
        }
    });

Finally, we concluded with this, the Press Space I added because when you commit that action of pressing space, I showed a still image of a green image or green background. I want to add a green colored background because I think it would calm the user down because green is the color of refreshing, of the color of lives with ree, a green space for user to calm down after looking at that crazy glitching screen.

Step 4: Final word
The process of making this was back and forth, I decided and have attempted to make a fractal tree but I don't like how it turned out to be. Luckily, glitch effect have so much areas to explores and during the process of making this, I have learnt a lot and with mistakes as well. I still believe there are a lot of areas that I can work on to make this code more interesting, I have tried to fix most of the mistakes and add more value for this one. I am happy with the result and looking forward to your opinion about this. See you on the next assignment.
