---
layout: page
title: colorizing the prokudin-gorskii photo collection
permalink: /projects/cs180/project1/
---

## background
[sergei mikhailovich prokudin-gorskii](https://en.wikipedia.org/wiki/Sergey_Prokudin-Gorsky) (1863-1944) traveled across the russian empire and captured photographs of everything! back then, there were no ways to print colored images, however, he was convinced that it would be possible someday in the future. from people and sculptures to buildings and trains, he recorded everything down on three glass plates with different exposures (red, green, and blue).

## overview
for this project, i use image processing techniques to take the digitized images prokudin-gorskii took, align them, and stack them together - basically recolorizing the images. this was done by the [library of congress](https://www.loc.gov/exhibits/empire/making.html).

before performing any sort of alignement, an important step of this process is to clean up any visual arjpgacts possible. this is crucial as it will create inaccuracies in our results when we perform caclulations in the later steps. to do this, i first divide the glass plate images into three equal parts **(r, g, b)** and then crop the borders by **10%**.

then, i will use one of the color channels (blue in my case) to act as an anchor while i shift the red and green channels around until they are all aligned.

### 1. single-scale search method
initially, i developed an algorithm which would exhaustively search a **[-15, -15]** pixels window of possible displacements. i would then calculate the normalized cross-correlation (ncc) to find the best score between the two images (blue and red/green) using the dot product of *im1/norm(im1) and im2/norm(im2)*. after that, i would take the displacement with the best ncc score and shift the image with respect to the blue image to align it nicely.

this method works well with lower resolution images (such as the .jpg images), however, when it comes to the larger resolution images (.tif images), this method proves to be computationally expensive as the search window would be much greater.

### 2. multi-scale pyramid search method
![multi-scale pyramid diagram](pyramid_example.png)
<p style="text-align: center; font-size: 12px"><i>image pyramid diagram with scaling factor 1/2</i></p>
<p style="text-align: center; font-size: 12px"><i>source: pyimagesearch</i></p>

to improve the efficiency of the algorithm, i implemented a new algorithm which uses an image pyramid. this algorithm basically scales down the original image multiple times to a coarser image where i can then use the single-scale search method and then slowly work our way up the pyramid shifting the images according to the displacement each time as i go.

this step is done recursively with a base case of *threshold=300px\*300px* and the search window becomes **[-2, 2]** pixels after the coarsest layer. the reason is because we would have already traversed up to a finer, shifted image (due to the *displacement \* 2* which is the scaling factor) where we would then only have to search a smaller neighborhood. in doing so, it significantly speeds up the computation time from an average of more than one minute to less than five seconds.

## results
- layout: original image, before alignment, after alignment
- displacements are in **(x, y)** format
<div class="image-gallery">
  <div class="image-container">
    <img src="results/monastery/original_monastery.jpg" alt="three channels of monastery" class="responsive-image"/>
    <img src="results/monastery/before_monastery.jpg" alt="image of monastery before processing" class="responsive-image"/>
    <img src="results/monastery/after_monastery.jpg" alt="image of monastery after processing" class="responsive-image"/>
  </div>
  <p>
    monastery.jpg<br>
    red channel:        (2, 3)<br>
    green channel:      (2, -3)<br>
    total time elapsed: 0.48s
  </p>

  <div class="image-container">
    <img src="results/tobolsk/original_tobolsk.jpg" alt="three channels of tobolsk" class="responsive-image"/>
    <img src="results/tobolsk/before_tobolsk.jpg" alt="image of tobolsk before processing" class="responsive-image"/>
    <img src="results/tobolsk/after_tobolsk.jpg" alt="image of tobolsk after processing" class="responsive-image"/>
  </div>
  <p>
    tobolsk.jpg<br>
    red channel:        (3, 6)<br>
    green channel:      (3, 3)<br>
    total time elapsed: 0.44s
  </p>

  <div class="image-container">
    <img src="results/cathedral/original_cathedral.jpg" alt="three channels of cathedral" class="responsive-image"/>
    <img src="results/cathedral/before_cathedral.jpg" alt="image of cathedral before processing" class="responsive-image"/>
    <img src="results/cathedral/after_cathedral.jpg" alt="image of cathedral after processing" class="responsive-image"/>
  </div>
  <p>
    cathedral.jpg<br>
    red channel:        (3, 12)<br>
    green channel:      (2, 5)<br>
    total time elapsed: 0.43s
  </p>

  <div class="image-container">
    <img src="results/emir/original_emir.jpg" alt="three channels of emir" class="responsive-image"/>
    <img src="results/emir/before_emir.jpg" alt="image of emir before processing" class="responsive-image"/>
    <img src="results/emir/after_emir.jpg" alt="image of emir after processing" class="responsive-image"/>
  </div>
  <p>
    emir.tif<br>
    red channel:        (-305, 93)<br>
    green channel:      (24, 49)<br>
    total time elapsed: 3.63s
  </p>

  <div class="image-container">
    <img src="results/church/original_church.jpg" alt="three channels of church" class="responsive-image"/>
    <img src="results/church/before_church.jpg" alt="image of church before processing" class="responsive-image"/>
    <img src="results/church/after_church.jpg" alt="image of church after processing" class="responsive-image"/>
  </div>
  <p>
    church.tif<br>
    red channel:        (-4, 58)<br>
    green channel:      (4, 25)<br>
    total time elapsed: 3.45s
  </p>

  <div class="image-container">
    <img src="results/three_generations/original_three_generations.jpg" alt="three channels of three generations" class="responsive-image"/>
    <img src="results/three_generations/before_three_generations.jpg" alt="image of three generations before processing" class="responsive-image"/>
    <img src="results/three_generations/after_three_generations.jpg" alt="image of three generations after processing" class="responsive-image"/>
  </div>
  <p>
    three_generations.tif<br>
    red channel:        (11, 112)<br>
    green channel:      (14, 53)<br>
    total time elapsed: 3.48s
  </p>

  <div class="image-container">
    <img src="results/melons/original_melons.jpg" alt="three channels of melons" class="responsive-image"/>
    <img src="results/melons/before_melons.jpg" alt="image of melons before processing" class="responsive-image"/>
    <img src="results/melons/after_melons.jpg" alt="image of melons after processing" class="responsive-image"/>
  </div>
  <p>
    melons.tif<br>
    red channel:        (13, 178)<br>
    green channel:      (10, 81)<br>
    total time elapsed: 3.27s
  </p>

  <div class="image-container">
    <img src="results/onion_church/original_onion_church.jpg" alt="three channels of onion church" class="responsive-image"/>
    <img src="results/onion_church/before_onion_church.jpg" alt="image of onion church before processing" class="responsive-image"/>
    <img src="results/onion_church/after_onion_church.jpg" alt="image of onion church after processing" class="responsive-image"/>
  </div>
  <p>
    onion_church.tif<br>
    red channel:        (36, 108)<br>
    green channel:      (26, 51)<br>
    total time elapsed: 3.28s
  </p>

  <div class="image-container">
    <img src="results/train/original_train.jpg" alt="three channels of train" class="responsive-image"/>
    <img src="results/train/before_train.jpg" alt="image of train before processing" class="responsive-image"/>
    <img src="results/train/after_train.jpg" alt="image of train after processing" class="responsive-image"/>
  </div>
  <p>
    train.tif<br>
    red channel:        (32, 87)<br>
    green channel:      (5, 42)<br>
    total time elapsed: 3.25s
  </p>

  <div class="image-container">
    <img src="results/icon/original_icon.jpg" alt="three channels of icon" class="responsive-image"/>
    <img src="results/icon/before_icon.jpg" alt="image of icon before processing" class="responsive-image"/>
    <img src="results/icon/after_icon.jpg" alt="image of icon after processing" class="responsive-image"/>
  </div>
  <p>
    icon.tif<br>
    red channel:        (23, 89)<br>
    green channel:      (17, 41)<br>
    total time elapsed: 3.28s
  </p>

  <div class="image-container">
    <img src="results/self_portrait/original_self_portrait.jpg" alt="three channels of self portrait" class="responsive-image"/>
    <img src="results/self_portrait/before_self_portrait.jpg" alt="image of self portrait before processing" class="responsive-image"/>
    <img src="results/self_portrait/after_self_portrait.jpg" alt="image of self portrait after processing" class="responsive-image"/>
  </div>
  <p>
    self_portrait.tif<br>
    red channel:        (37, 176)<br>
    green channel:      (29, 78)<br>
    total time elapsed: 3.37s
  </p>

  <div class="image-container">
    <img src="results/harvesters/original_harvesters.jpg" alt="three channels of harvesters" class="responsive-image"/>
    <img src="results/harvesters/before_harvesters.jpg" alt="image of harvesters before processing" class="responsive-image"/>
    <img src="results/harvesters/after_harvesters.jpg" alt="image of harvesters after processing" class="responsive-image"/>
  </div>
  <p>
    harvesters.tif<br>
    red channel:        (13, 124)<br>
    green channel:      (16, 59)<br>
    total time elapsed: 3.17s
  </p>

  <div class="image-container">
    <img src="results/sculpture/original_sculpture.jpg" alt="three channels of sculpture" class="responsive-image"/>
    <img src="results/sculpture/before_sculpture.jpg" alt="image of sculpture before processing" class="responsive-image"/>
    <img src="results/sculpture/after_sculpture.jpg" alt="image of sculpture after processing" class="responsive-image"/>
  </div>
  <p>
    sculpture.tif<br>
    red channel:        (-27, 140)<br>
    green channel:      (-11, 33)<br>
    total time elapsed: 3.33s
  </p>

  <div class="image-container">
    <img src="results/lady/original_lady.jpg" alt="three channels of lady" class="responsive-image"/>
    <img src="results/lady/before_lady.jpg" alt="image of lady before processing" class="responsive-image"/>
    <img src="results/lady/after_lady.jpg" alt="image of lady after processing" class="responsive-image"/>
  </div>
  <p>
    lady.tif<br>
    red channel:        (12, 111)<br>
    green channel:      (9, 51)<br>
    total time elapsed: 3.26s
  </p>
</div>


<style>
  .image-gallery {
    max-width: 100%;
    overflow-x: auto;
    text-align: center;
  }
  
  .image-container {
    display: inline-flex;
    jusjpgy-content: center;
    gap: 10px;
    padding: 10px;
    max-width: 100%;
  }
  
  .image-container img {
    height: 220px; /* Adjust this value as needed */
    width: auto;
    object-fit: contain;
  }
  
  @media (max-width: 768px) {
    .image-container {
      flex-direction: column;
      align-items: center;
    }
    
    .image-container img {
      max-width: 100%;
      height: auto;
    }
  }
</style>