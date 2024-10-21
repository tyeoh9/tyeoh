---
layout: page
title: image warping and mosaicing
permalink: /projects/cs180/project4/
---

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/blended_mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>a mosaic of the heyns reading room at uc berkeley</i>
</div>

## part a:

### background

imagine stitching together photos seamlessly, like creating panoramas on your phone or the immersive scenes in vr headsets. this project dives into image mosaicing, where multiple images are registered, projectively warped, resampled, and composited into a single, cohesive mosaic. by computing homographies and warping images, i explored key techniques used in modern camera apps and augmented reality systems.

### shooting the pictures

the pictures below were shot with my iphone camera with the camera itself being the center of projection; the camera acted as a pivot as i slowly turned my camera and snapped some photos. this is important for when we warp our images and stitch them together to minimize errors and artifacts. currently, these images are in its **raw and original form** where they will later on be projected onto the center image via the projection transformation matrix.

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/orig/tennis_left.JPG" style="height: 250px"/>
        <img src="tennis/orig/tennis_mid.JPG" style="height: 250px"/>
        <img src="tennis/orig/tennis_right.JPG" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>hearst tennis courts at uc berkeley on a saturday morning</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/orig/heyns_left.JPG" style="height: 250px"/>
        <img src="heyns/orig/heyns_mid.JPG" style="height: 250px"/>
        <img src="heyns/orig/heyns_right.JPG" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>the roger w. heyns reading room at uc berkeley</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/orig/street_left.JPG" style="height: 250px"/>
        <img src="street/orig/street_mid.JPG" style="height: 250px"/>
        <img src="street/orig/street_right.JPG" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>some pictures of the street outside my apartment</i>
</div>

### recover homographies

to recover the homographies of the images, we simply find the transformation `p' = Hp` where **H** is a 3x3 matrix with 8 degrees of freedom. in my code, i use the function 
```
H = computeH(im1_pts,im2_pts)
```
 to compute matrix **H** where *im1_pts* and *im2_pts* are the corresponding **(x, y)** points of two images. the homography matrix can be solved by recovering the 8 parameters as seen by solving the following equation:

<div class="image-wrapper">
    <div class="image-container">
        <img src="homographies/proj_transform.png" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>solving for the projection transformation matrix</i>
</div>

we can then expand this out to solve for the parameters *a to h*:

<div class="image-wrapper">
    <div class="image-container">
        <img src="homographies/least_squares.png" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>solve via least squares</i>
</div>

this solves for a pair of corresponding points. to solve for more corresponding points, we simply just stack the matrix on the left vertically.

### warp the images

we can use the `computeH()` function to find the homographies of different images. in our case we will project the left and right images onto the middle image. we can then later use these images and stitch them together to form an image mosaic! as seen in lecture, inverse warping produces better results as it doesn't result in holes in the final image; we use this for our function
```
imwarped = warpImage(im,H)
```
it is important to note that after warping the points of one image to another, we might encounter some values in negative locations. to deal with this, we keep track of the displacement of the warped image from the original image and apply the translation *dx* and *dy* to the warped image. furthermore, the warped image may not necessarily be the same size as the original image which is why we first find the 'boundaries' of the warped corners and then create a new canvas with the newly obtained dimension of the image.

#### corresponding points

below is the visualization of the corresponding points for one of our soon-to-be mosaic

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/left_pts.jpg" style="height: 300px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>a visualization of the corresponding points of the tennis courts (right to mid)</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/right_pts.jpg" style="height: 300px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>a visualization of the corresponding points of the tennis courts (left to mid)</i>
</div>

#### below are some results of the warped images:

tennis courts:

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/orig/tennis_left.JPG" style="height: 350px"/>
        <img src="tennis/left_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original left image vs warped image</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/orig/tennis_right.JPG" style="height: 350px"/>
        <img src="tennis/right_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original right image vs warped image</i>
</div>

heyns reading room:

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/orig/heyns_left.JPG" style="height: 350px"/>
        <img src="heyns/left_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original left image vs warped image</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/orig/heyns_right.JPG" style="height: 350px"/>
        <img src="heyns/right_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original right image vs warped image</i>
</div>

street:

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/orig/street_left.JPG" style="height: 350px"/>
        <img src="street/left_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original left image vs warped image</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/orig/street_right.JPG" style="height: 350px"/>
        <img src="street/right_warped.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original right image vs warped image</i>
</div>

### image rectification

to test that our warp function is working so far, i perform rectification on some other images that i took and some from the web. i select corner points from the object in the image that i would like to rectify and since i know the ground plane rectification, i can select the corner points that will be rectified. below are some of the original images, the corresponding points, as well as the rectified (cropped) images.

#### art gallery (weitman gallery, washington university):

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/gallery.jpg" style="height: 350px"/>
        <img src="rectification/gallery_pts.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original image vs original image with points</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/gallery_rect.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>rectified image of the artwork on the wall</i>
</div>

#### taking a peek at my roommate's homework:

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/homework.jpg" style="height: 350px"/>
        <img src="rectification/homework_pts.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original image vs original image with points</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/homework_rect.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>a sneaky rectified image of my roommate's homework</i>
</div>

#### berkeley magazine on the coffee table:

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/magazine.jpg" style="height: 350px"/>
        <img src="rectification/magazine_pts.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>original image vs original image with points</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="rectification/magazine_rect.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>rectified version of berkeley engineering magazine</i>
</div>

now that we know our *warpImage()* function works, we can move on to creating our image mosaics of the photographs we took before!

### blend the images into a mosaic

using our previously warped images (tennis courts, heyns reading room, and my street view), we can stitch those warped images together, perform some blending, and we will end up with a panorama!

below are the results of placing the warped (left and right) images beside the (unwarped) center image via translation onto a large canvas:

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of tennis courts without blending</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of heyns reading room without blending</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of the street without blending</i>
</div>

the results are pretty good! we can see that the images are aligned. but, there's an issue. the edges where the separate images meet are very strong and we can tell that these are separate image put side-by-side, not a mosaic. 

to fix this, we use what we did in the [image blending project](../project2/project2.md) and use a level-2 laplacian pyramid to blend the seams together. i first blend the warped left image to the center, then the warped right image to the center, and then blend both of those blended images together. the results are here:

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/blended_mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of tennis courts</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/blended_mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of heyns reading room</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/blended_mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of the street</i>
</div>

you can see the huge improvement in the images! the seams are now gone - we have created panoramas from 3 different photographs.

<style>
    .image-gallery {
        max-width: 100%;
        overflow-x: auto;
        text-align: center;
    }
    
    .image-container {
        display: inline-flex;
        justify-content: center;
        gap: 10px;
        padding: 10px;
        max-width: 100%;
        text-align: center;
    }
    
    .image-container img {
        height: 220px; /* Adjust this value as needed */
        width: auto;
        object-fit: contain;
    }
    
    .image-wrapper {
        text-align: center; /* Ensures everything inside is centered */
        width: 100%;
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