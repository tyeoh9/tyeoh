---
layout: page
title: projects
permalink: /projects/
---

### [gpt traffic monitor assistant](https://github.com/tyeoh9/GPT4oVisionTrafficMonitor)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/part2_ui.png"/>
    </div>
</div>

### [non-photorealistic shader](https://github.com/tyeoh9/NPRRenderer)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/link.gif"/>
    </div>
</div>

### [neural radiance fields (NeRF)](/projects/cs180/project6/project6.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project6/part2/nerf_output/iter125.jpg" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project6/part2/nerf_output/iter350.jpg" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project6/part2/nerf_output/iter750.jpg" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project6/part2/final_render/final.gif" style="height: 150px"/>
    </div>
</div>

### [the power of diffusion models](/projects/cs180/project5/project5.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project5/part_a/part7_2/test_orig.png" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project5/part_a/part7_2/test_mask.png" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project5/part_a/part7_2/test_replace.png" style="height: 150px"/>
        <img src="{{ site.baseurl }}/projects/cs180/project5/part_a/part7_2/test_inpaint3.png" style="height: 150px"/>
    </div>
</div>

### [image warping and mosaicing](/projects/cs180/project4/project4.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project4/heyns/blended_mosaic.jpg"/>
    </div>
</div>

### [face morphing](/projects/cs180/project3/project3.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project3/kanye.jpg"/>
        <img src="{{ site.baseurl }}/projects/cs180/project3/part3_results/morphed_kanye_thomas-ezgif.com-loop-count.gif"/>
        <img src="{{ site.baseurl }}/projects/cs180/project3/thomas.jpg"/>
    </div>
</div>

### [convolutions, filters, and frequencies](/projects/cs180/project2/project2.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project2/results/blending/apple.jpeg"/>
        <img src="{{ site.baseurl }}/projects/cs180/project2/results/blending/orange.jpeg"/>
        <img src="{{ site.baseurl }}/projects/cs180/project2/results/blending/oraple.jpg"/>
    </div>
</div>

### [colorizing the prokudin-gorskii photo collection](/projects/cs180/project1/project1.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/cs180/project1/results/harvesters/original_harvesters.jpg"/>
        <img src="{{ site.baseurl }}/projects/cs180/project1/results/harvesters/before_harvesters.jpg"/>
        <img src="{{ site.baseurl }}/projects/cs180/project1/results/harvesters/after_harvesters.jpg"/>
    </div>
</div>

### [build your own world (byow): an engine for generating explorable worlds](https://github.com/tyeoh9/BYOW)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/gameplay.gif"/>
    </div>
</div>

### [text classification application](/projects/text-app/text-app.md)

<div class="image-wrapper">
    <div class="image-container">
        <img src="{{ site.baseurl }}/projects/text-app/screenshots/predictions_page.png"/>
    </div>
</div>

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
        text-align: center; Ensures everything inside is centered
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