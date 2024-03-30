---
title:  Assignment 1 Blog
published_at: 2024-03-30
snippet: Assignment 1 recap and understanding
disable_html_sanitization: true
---
# Assignment 1 Recap Blog
## Here is my process of thinking and developing Assignment 1

Prior to this assignment, I had to learn and understand the concept of effective complexity and cute from Sianne Ngai’s book, which was the baseline and the core concept for this assignment. In addition to the two concepts, I need to incorporate them with the inspiration of Rafael Rozendaal's artwork. Ever since the first week, I have been practicing how to “mimic” his work and practice week by week. Rozen daal's work is not easy to mimic and this is the first time I have worked with code hence I have a bit of issues when learning and understanding all these new concepts. I watched many tutorials and have seen examples from the p5js library to try and solve for the right code. A lot of times I could not get it right but I have to move on to other classes and materials as well. In the end, with all the materials that I have understood I move on to sketch for this assignment.

Firstly, for week 3 homework, I was told to look at one of Rozendaal's works and I chosen “pink yellow blue”. I like the simplicity and cuteness of the color and the behavior of the two objects but still have the effective complexity of the randomness in movement and chaos when they collide and change colors. From that, I wanna have a sketch with all of those elements combined. since we are focusing mainly on the topic of cute, and as Sianne Ngai said cute can assumed to be manipulative and also vulnerable.  Then I think of waves as an example because I think waves can be broken easily when met with obstacles like the concept of how others assume about cute. I started building my sketch upon that thought and I took another inspiration from “trying trying” and “falling falling”.[https://www.fallingfalling.com/] [https://www.fallingfalling.com/] Those two examples from my point of view have the vision of a wave but seeing upfront but since I already have the code for “falling falling” I would like to do something better. 

Secondly, I started to find examples from the internet starting with the p5js library and Youtube. In the library, I found out there is a wavemaker code that was already built and I did try it out for inspiration.


```
let t = 0; // time variable

function setup() {
  createCanvas(600, 600);
  noStroke();
  fill(40, 200, 40);
}

function draw() {
  background(10, 10); // translucent background (creates trails)

  // make a x and y grid of ellipses
  for (let x = 0; x <= width; x = x + 30) {
    for (let y = 0; y <= height; y = y + 30) {
      // starting point of each circle depends on mouse position
      const xAngle = map(mouseX, 0, width, -4 * PI, 4 * PI, true);
      const yAngle = map(mouseY, 0, height, -4 * PI, 4 * PI, true);
      // and also varies based on the particle's location
      const angle = xAngle * (x / width) + yAngle * (y / height);

      // each particle moves in a circle
      const myX = x + 20 * cos(2 * PI * t + angle);
      const myY = y + 20 * sin(2 * PI * t + angle);

      ellipse(myX, myY, 10); // draw particle
    }
  }

  t = t + 0.01; // update time
}
```

 Moving to YouTube, I found multiple tutorials, which helped me to understand the concept further. I found Patt Vira's tutorial on how to make a wave pattern and learned from her then.
 <iframe width="560" height="315" src="https://www.youtube.com/embed/DNZPyoMBiFw?si=u8zOMv2nekdR75x6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
Vira’s explanation is simple but details due to her experience so I understand most of the materials due to some of the materials requiring higher understanding. The tutorial helped me understand more information and materials hence my demo was created.
sketch.js demo
```
let c;
let grid=[]; 
let cols=20;
let rows=20;
let loc=50; 

function setup() {
  createCanvas(innerWidth,innerHeight);
let rowSize=height/rows;
let colSize=width/cols;
    
  for (let i=0; i<cols; i++){
    grid[i]=[]; 
    for (let j=0; j<rows; j++){
      grid[i][j]=new Cell(colSize/2+i*colSize,rowSize/2+j*rowSize, rowSize/2, i*loc+j*loc);// spacing of the circles

    }
  }
}

function draw() {
  background(0);
 for (let i=0; i<cols; i++){
    for (let j=0; j<rows; j++){
      grid[i][j].update();
      grid[i][j].display();
      
    }
  }
}
```
cell class demo

```
class Cell{ //create a class for the circle cell
  constructor(x0,y0, r, angle){ 
//x0 and y0 are the center of the circle in motion
    this.r=90; //radius of the circke
    this.angle= angle;
    this.x0 = x0;
    this.y0 = y0;
  }
  update(){ //update the location of the circle
    this.x=this.r*cos(this.angle);
    this.y=this.r*sin(this.angle);
    this.angle += 0.01; 
  }
  
  display(){ //drawing the circle cell
    fill(this.color);
    // ellipse(this.x0, this.y0, this.r*2, this.r*2);
    // line(this.x0,this.y0, this.x0+this.x,this.y0+this.y);
    ellipse( this.x0+this.x, this.y0+this.y,15,15);
    
  }
}
```
<iframe src="https://editor.p5js.org/khoanguyen1111/full/aN8_YN4Wx"width="100%"></iframe>

 Although, her tutorial was amazing however the result was not the one I wanted to create. I wanted to add vibrant color to this plain black-and-white background. I looked up a tutorial on how to add random colors to the circle and the background. Since I created randomness hence I decided to choose random colors for the wave circle so that every time user refreshes it will be a new set of waves. I added the noStroke function to the code so that it does not have the black trails behind but the trails will be to the colors of the dot.



Lastly, I fixed the leftover code and styled it so that it would be well-presented to look at and added comments so that people could understand what is the meaning of the code. I look back at my code and I am happy with what I understand and put my knowledge into this assessment. Even though I am happy I can’t wait to listen to all the feedback since I know that I made one are many mistakes in this assignment, so that I can improve in the future assessment.

Here is what I did, take a look!
<iframe src="https://editor.p5js.org/khoanguyen1111/full/bCslGQyPm" width="100%" height="50%"></iframe>