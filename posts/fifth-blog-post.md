---
title: 5th blog post hehe
published_at: 2024-03-29
snippet: making glitch portrait
disable_html_sanitization: true
---

<canvas id="glitch_self_portrait"></canvas>

<script type="module">
//create a canvas
   const cnv = document.getElementById (`glitch_self_portrait`)

   //sizing to be good size
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16
   //background color
   cnv.style.backgroundColor = `deeppink`  
   //canvas context
   const ctx = cnv.getContext (`2d`)

    //installing variable for image data
   let img_data

//defining a function that draw the image
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height)
//creating a new image
   const img = new Image ()
   // define function to execute loading file
   img.onload = () => {

    //resizing the image size

      cnv.height = cnv.width * (img.height / img.width)
      //draw image
      draw (img)
        // storing image date as string in img_data
      img_data = cnv.toDataURL ("image/jpeg")
      //call the glitch function
      add_glitch ()
   }
   //give filepath to image element

   img.src = `/demo.JPG` //add my own picture

    //define a function that returns a random value between 0-max
   const rand_int = max => Math.floor (Math.random () * max)
    // define a recursive function
   const glitchify = (data, chunk_max, repeats) => {
    //random multiple of 4 between 0-chunk_max
      const chunk_size = rand_int (chunk_max / 4) * 4

    // random position in the data between 24-chunk_size
      const i = rand_int (data.length - 24 - chunk_size) + 24
      //grabing all data before the random position
      const front = data.slice (0, i)
      // leaaving a gap the size of chunk_size
      //grabbing the rest of the data
      const back = data.slice (i + chunk_size, data.length)
      //putting two pieces back together
      //leaving out a chunk
      const result = front + back

      //ternary operator to return result if false
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }
    //instanitate empty array for glitched images
   const glitch_arr = []
    
    //define function that adds glitch imnage
    // to the glitch array
   const add_glitch = () => {

    //make new image element
      const i = new Image ()
      // define function that executes when image receives its data
      i.onload = () => {
        //push the image into the glitch_arr array
         glitch_arr.push (i)
         //call itself until there are 12 glitched images
         if (glitch_arr.length < 12) add_glitch ()
         //once there 12 images, start animating
         else draw_frame ()
      }

      //give the new image some glith effect image data
      i.src = glitchify (img_data, 96, 6)
   }

    // instanitate variable to keep track of glitch state
   let is_glitching = false
   // keep track of which glitch image from the arrat we are using
   let glitch_i = 0


   const draw_frame = () => {
    // check the glitch
    // if glitching draw the glitch array image
      if (is_glitching) draw (glitch_arr[glitch_i])
      //otherwise draw the regular image
      else draw (img)
      
    //probability weighting for starting and stopping the glitch
      const prob = is_glitching ? 0.05 : 0.02
      //if random value is less than weight value
      if (Math.random () < prob) {
        //chooose a random glitch image index
         glitch_i = rand_int (glitch_arr.length)
         //flip the state of is_glitching
         is_glitching = !is_glitching
      }

        //call the next animation frame
      requestAnimationFrame (draw_frame)
   }

 </script>

```
<canvas id="glitch_self_portrait"></canvas>

<script type="module">
  const cnv = document.getElementById(`glitch_self_portrait`);
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;
  cnv.style.backgroundColor = `deeppink`;

  const ctx = cnv.getContext(`2d`);

  let img_data;

  const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    draw(img);
    img_data = cnv.toDataURL("image/jpeg");
    add_glitch();
  };
  img.src = `/demo.jpg`;

  const rand_int = (max) => Math.floor(Math.random() * max);

  const glitchify = (data, chunk_max, repeats) => {
    const chunk_size = rand_int(chunk_max / 4) * 4;
    const i = rand_int(data.length - 24 - chunk_size) + 24;
    const front = data.slice(0, i);
    const back = data.slice(i + chunk_size, data.length);
    const result = front + back;
    return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
  };

  const glitch_arr = [];

  const add_glitch = () => {
    const i = new Image();
    i.onload = () => {
      glitch_arr.push(i);
      if (glitch_arr.length < 12) add_glitch();
      else draw_frame();
    };
    i.src = glitchify(img_data, 96, 6);
  };

  let is_glitching = false;
  let glitch_i = 0;

  const draw_frame = () => {
    if (is_glitching) draw(glitch_arr[glitch_i]);
    else draw(img);

    const prob = is_glitching ? 0.05 : 0.02;
    if (Math.random() < prob) {
      glitch_i = rand_int(glitch_arr.length);
      is_glitching = !is_glitching;
    }

    requestAnimationFrame(draw_frame);
  };
</script>
```
