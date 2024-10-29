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

to fix this, we use what we did in the [image blending project](../project2/project2.md) and use a level-2 laplacian pyramid to blend the seams together. i first blend the warped left image to the center, then the warped right image to the center, and then blend both of those blended images together. here are the level-2 laplacian pyramid masks i used for the heyns panoramas:

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/mask_left.jpg" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/mask_mid.jpg" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/mask_right.jpg" style="height: 250px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>masks of used for blending the heyns images</i>
</div>

#### the final results are here:

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/blended_mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>mosaic of tennis courts [note: the reason for the distinct color difference is due to the images itself and the lighting of when they were taken]</i>
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

## part b: feature matching and autostitching

even though our mosaics turned out pretty nice, much of the process is very manual. picking the correspondence points itself takes a while. in this part of the project, i will implement feature matching and autostitching to create our mosaics for us.

### corner detection

similar to how i manually selected the points, we want to select corner points by using the harris interest point detector. the harris interest point detector uses peaks in the matrix to find corners.

below are images of harris points overlaid onto my photos:

#### no threshold (all harris points):

<div class="image-wrapper">
    <div class="image-container">
        <img src="harris_points/left_pts_no_thresh.jpg" style="height: 350px"/>
        <img src="harris_points/mid_pts_no_thresh.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>heyns (left), heyns (mid)</i>
</div>

but you can see that there are way too many points. let's set a threshold to only keep the top n points.

#### threshold = 2000:

<div class="image-wrapper">
    <div class="image-container">
        <img src="harris_points/left_pts_tresh2000.jpg" style="height: 350px"/>
        <img src="harris_points/mid_pts_thresh2000.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>heyns (left), heyns (mid)</i>
</div>

#### threshold = 1000:

<div class="image-wrapper">
    <div class="image-container">
        <img src="harris_points/left_pts_tresh1000.jpg" style="height: 350px"/>
        <img src="harris_points/mid_pts_thresh1000.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>heyns (left), heyns (mid)</i>
</div>

using a threshold to filter out the top n corners is a good idea but it is not very sophisticated. you can see in our above images that our corners are not very spaced out; we get clusters spread out sparsely throughout the image.

### adaptive non-maximal suppression (anms)

with the harris interest points, we get lots of redudant information since many points are clustered together. to space out the points a little more, we use adaptive non-maximal suppression (anms) to make our feature matching more effective.

i implemented the algorithm from section 3 of the paper ["multi-image matching using multi-scale oriented patches" by brown et al.](https://inst.eecs.berkeley.edu/~cs180/fa24/hw/proj4/Papers/MOPS.pdf).

you can see my anms points overlaid onto the images below. you can observe that the points are a lot more evenly spread out compared to just using the threshold:

#### 500 anms points:

<div class="image-wrapper">
    <div class="image-container">
        <img src="anms/im_left_ANMS_n500.jpg" style="height: 350px"/>
        <img src="anms/im_mid_ANMS_n500.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>heyns (left), heyns (mid)</i>
</div>

### extracting feature descriptors

before we can match our correspondence points, we need to get some context for each point and to do this, we use feature descriptors. for each points, we get its feature descriptor which is a sample of 40x40 pixels centered around that pixel and downsize (space it out) by s=5 (resulting sample will be 8x8). after we do this, we have to bias/gain-normalize our descriptors. here are some of the descriptors from the heyns reading room images.

#### point at (x=683, y=546):

<div class="image-wrapper">
    <div class="image-container">
        <img src="feature_descriptors/bw_window_x683_y546.jpg" style="height: 200px"/>
        <img src="feature_descriptors/bw_descriptor_x683_y546.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_window_x683_y546.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_descriptor_x683_y546.jpg" style="height: 200px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>40x40 sample window vs 8x8 descriptor (in both b&w and color)</i>
</div>

#### point at (x=856, y=1041):

<div class="image-wrapper">
    <div class="image-container">
        <img src="feature_descriptors/bw_window_x856_y1041.jpg" style="height: 200px"/>
        <img src="feature_descriptors/bw_descriptor_x856_y1041.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_window_x856_y1041.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_descriptor_x856_y1041.jpg" style="height: 200px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>40x40 sample window vs 8x8 descriptor (in both b&w and color)</i>
</div>

#### point at (x=893, y=930):

<div class="image-wrapper">
    <div class="image-container">
        <img src="feature_descriptors/bw_window_x893_y930.jpg" style="height: 200px"/>
        <img src="feature_descriptors/bw_descriptor_x893_y930.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_window_x893_y930.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_descriptor_x893_y930.jpg" style="height: 200px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>40x40 sample window vs 8x8 descriptor (in both b&w and color)</i>
</div>

#### point at (x=1277, y=1034):

<div class="image-wrapper">
    <div class="image-container">
        <img src="feature_descriptors/bw_window_x1277_y1034.jpg" style="height: 200px"/>
        <img src="feature_descriptors/bw_descriptor_x1277_y1034.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_window_x1277_y1034.jpg" style="height: 200px"/>
        <img src="feature_descriptors/colored_descriptor_x1277_y1034.jpg" style="height: 200px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>40x40 sample window vs 8x8 descriptor (in both b&w and color)</i>
</div>

### feature matching between two images

we use the feature descriptors from both images and find the closest corresponding descriptors to match to each other. we implement section 5 of brown's paper in this part of the project. we also make use of lowe's trick for thresholding by setting the threshold to the ratio between the nearest and second-nearest neighbor.

<div class="image-wrapper">
    <div class="image-container">
        <img src="feature_matching/corresponding_points_41_matches.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>corresponding points between both images; # matched points: 41</i>
</div>

### 4-point random sample consensus (ransac)

lowe's trick improves the matching process by reducing the number of outliers. however, we will evidently still have some outliers remaining which can really skew our calculations when finding the least-squares solution. just one pair of incorrect points can really mess up the homography matrix calculations. this is why we need to use ransac.

the general idea of ransac:
1. select four feature pairs (at random)
2. compute homography H (exact)
3. compute inliers where `dist(pi’, Hpi) < ε`
4. keep largest set of inliers
5. re-compute least-squares H estimate on all of the inliers

we can see below that ransac does a really good job at eliminating the outliers:

<div class="image-wrapper">
    <div class="image-container">
        <img src="ransac/im_left_RANSAC.jpg" style="height: 350px"/>
        <img src="ransac/im_mid_RANSAC.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>points matched by ransac are in red; you can see that this has significantly reduced the number of outliers, only keeping the ransac points</i>
</div>

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/left_warped.jpg" style="height: 350px"/>
        <img src="ransac/warped_left.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>warped image (by manual correspondence), warped image (by ransac)</i>
</div>

you can see that the homography **H** produced by ransac is pretty accurate as the warped image from both manually and automatically selected points are the same.

### autostitching (putting everything together)

#### heyns

<div class="image-wrapper">
    <div class="image-container">
        <img src="heyns/blended_mosaic.jpg" style="height: 350px"/>
        <img src="autostitch/heyns/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>heyns reading room with manual correspondences (left) vs automatic correspondences (right)</i>
</div>

you can see that the results are really good! they are basically identical. if we zoom in a little more, into both images, we can see that there are minor differences.

<div class="image-wrapper">
    <div class="image-container">
        <img src="autostitch/heyns/zoomed_manual.jpg" style="height: 350px"/>
        <img src="autostitch/heyns/zoomed_auto.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>zoomed image of manual correspondence vs automatic correspondence</i>
</div>

you can see that the automatic correspondence points using all the techniques used in the second part of the project actually does a better job than manually selected points (as expected). in the image on the left (manual correspondences), there are some noticeable artifacts while there are none in the image on the right.

<div class="image-wrapper">
    <div class="image-container">
        <img src="autostitch/heyns/zoomed_manual2.jpg" style="height: 350px"/>
        <img src="autostitch/heyns/zoomed_auto2.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>zoomed image of manual correspondence (left) vs automatic correspondence (right)</i>
</div>

#### tennis

<div class="image-wrapper">
    <div class="image-container">
        <img src="tennis/blended_mosaic.jpg" style="height: 350px"/>
        <img src="autostitch/tennis/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>tennis courts with manual correspondences (left) vs automatic correspondences (right)</i>
</div>

#### street view

<div class="image-wrapper">
    <div class="image-container">
        <img src="street/blended_mosaic.jpg" style="height: 350px"/>
        <img src="autostitch/street/mosaic.jpg" style="height: 350px"/>
    </div>
</div>
<div class="image-wrapper">
    <i>street view with manual correspondences (left) vs automatic correspondences (right)</i>
</div>

## closing remarks

this project encompasses many techniques we learned in our past assignmnets and combines them all into a single project. it is also quite fascinating to see how much can be done in image processing with just mathematics and smart tricks/techniques. 

being able to automate the process of selecting correspondence points and stitching/blending the images together has been both satisfying and rewarding. :)

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