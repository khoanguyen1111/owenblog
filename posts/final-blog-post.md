---
title: The Finale
published_at: 2024-06-16
snippet: AT3 Reflection
disable_html_sanitization: true
---

# Here we are, at our last assignment

## LETS BREAK IT DOWNNNN

<iframe src="https://editor.p5js.org/khoanguyen1111/full/TeTNmgNCa"></iframe>

So here is my final assignment, for me it was a weird thinking process because it was not the idea that I had initially but an idea that came up while I was searching for a solution. From the top, I had this idea of creating an audio visualizer because back when I was a kid I found that my PC had this application can visualize audio. Every beat and every drums and every hi hats has an effects on the visualizer. You don't even know how many times I look and find for that function again. However, as a kid, my time at the PC table were limited as my parents put sports and academic above all, which I wish I could have learn more about but it was ok. So that was the idea. Going to year 1 of Design major, I saw how people did it, but not with the code but with others materials and applications. Hence I know it is possible to create that I google how to do that but with code.

I found the tutorial but I thought to myself "oh but what is my domain? the audio visualizer group? And who is my repetoire?". I hit a hard stop, but then I found this video tutorial of this lady of making p5js character moves by sound(https://www.youtube.com/watch?v=b_dmlTqVov8). I was hooked because I know that there are a community that would have interest in this. As the online persona are as important as your real life persona and could be more important for some people, security is also important. On Youtube and other platforms, content creator are now using an animated character to visualize their movement and persona without showing the viewers their actual face. Hence, I started to grab my pots and pans and went staright to cooking.

Here is a break down of how I did it and improve on that as well

First of all, I created two variables, mic and volume. Mic is to create a mic input so that the web will allow microphone and then capture to the p5js code. Volume is to control how sensitive the volume of your voice, in a way your sensitivity in sound so that the character can move .

```
let mic; // allows to use sound from desktop microphone
let vol; // allows to change volume
let circles = []; // array to hold circles

function setup() {
createCanvas(innerWidth,innerHeight);
colorMode(HSB);

mic = new p5.AudioIn();
mic.start();
mic.amp(8.0);

// Initialize circles
for (let i = 0; i < 100; i++) {
circles.push({
x: random(width),
y: random(height),
size: random(10, 50),
hue: random(360),
maxRadius: random(30, 100),
angle: random(TWO_PI), // Initial random angle
rotationSpeed: random(-0.05, 0.05) // Random rotation speed
});
}
}
```

I also created an array of circles so that let me to add depth to the background and it also reactive to the sound of my mic. The code is straightforward with the comments but however, I want to talk about mic amp. During the process I could not find a way to increase the sensitivity even though I changed the main circles volume. Hence mic.amp is to amplified the sensitivy of the whole code so that the sound will be louder without speaking so loud. A downside is that the sound is really reactive, if you whispered, it reacts which I was not asking for it but it worked so I don't mind. I then initialized the circles to make it randomly appears after every reload and the circles would be popping up and down => reactively. Now we are gonna talk about the second part of the code, the draw function.

Let's start simple, the face and making the mouth reactive to sound.

```
// Draw the main circle
  fill(50, 41, 93);
  circle(width / 2, height / 2, height * 0.9);

  // Draw the eyes
  fill(0);
  circle(width / 3 + width * 0.05, height / 2 - width * 0.05, width * 0.05);
  circle(width / 2 + width * 0.1, height / 2 - width * 0.05, width * 0.05);

  // Draw the mouth
  arc(width / 2, height / 2, width / 3, width * 0.03 + vol * width * 0.9, 0, PI, CHORD);
}
```

```
 vol = mic.getLevel(); // Get volume level from microphone
```

All of the information I written down here is from the p5js references page and I have realized that I have never used it to its abilities. It helped me with basic more then the video tutorial and now I wished that I use the references page more on my first assignment. If we look at the arc function to draw the mouth, to be able to make it "talk" I have to add the vol variable so that it would move. The number that vol multiply with is the function that increase the sensitivity of the mic but as I explained, yeahhh.... it didn't work to my liking. A better solution was found and I am happy (it works sooo gooooddd)

```
background(221, 70, 66); // Set background color

  // Update and draw reactive background circles
  for (let i = 0; i < circles.length; i++) {
    let circle = circles[i];

    // Update angle based on rotation speed
    circle.angle += circle.rotationSpeed;

    // Change size based on volume
    let maxSize = circle.maxRadius + vol * 300;
    let newSize = map(sin(frameCount * 0.1), -1, 1, circle.size, maxSize);

    let hueOffset = map(circle.y, 0, height, 0, 100);
    let hue = (circle.hue + hueOffset) % 360;

    fill(hue, 100, 100);
    noStroke();

    // Making the cirlce pop
    push();
    translate(circle.x, circle.y);
    rotate(circle.angle);
    ellipse(0, 0, newSize, newSize);
    pop();
  }
```

Now we talk about the background elements that I have inmplemented. There are two things I want to achive for the background elements, 1st is that it has to spawn at random location after everytime, 2nd is that it has to react to the microphone input. Once again, I also add the vol varible into the circle max size function so that the size when I scream, it will be big and "overreacte" in a way to the sound. Making the circle pop, by using the push and pop function. During the idea coming up of this idea, I was having trouble to make it pop to my liking, I looked for a example on ChatGPT in able to find a solution to my liking and it explain by push and pop to transform it shapes and sizes. Translate, rotate are the two function that making the function expand and translate so that they would be popping as they idle waiting for the sound input.

After all in that working in harmony, our final product is a wonderful yellowball that like to interact with peopel. I can say what the opinion are about my project but I do find this project is interesting because not of how I can make the idea in my head becomes something more than my sketch ideas. It was like a version of McCarthy project during the Covid times but now since we do noy have Covid anymore and online socials are important, a solution comes up to keep your identity safe but also still have emotions without being lost in translation.

As my final words, I would like to say that I am more than happy to have been in this class. I am behind my any means due to my lack of experience in coding but with the help of my peers and especially my instructor who bares with me even though I have minimal skills in class, he still helps me. I am grateful for the experience and I am thankful for taking this class. What a semester it has been.
