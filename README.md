# Animate Plug-in for Unreal

*made in Unreal 5.4* by [Elina Timermane](https://www.linkedin.com/in/elina-timermane/)

## Table of Contents
1. [Introduction](#introduction)
2. [Plug-in Content](#plug-in-content)
3. [Set Up](#set-up)
4. [Important](#important)
5. [Eases](#eases)
6. [Presets](#presets)
7. [World VS Relative Transform](#world-vs-relative-transform)
   <br><be>

## Introduction

Animate plug-in helps to simplify the object animation process, reducing functionality to one node meanwhile maintaining variety and customisation. 

Here’s a complete guide to the plugin, explaining all available functionality.

But first, why animate? 

Animate speeds up the animation process, and makes it more designer-friendly (compared to Unreal’s Timeline, which requires additional logic) and is still highly customisable.  

Completely made in **blueprints** - it doesn’t require the inclusion of C++ into your Unreal project as most tween plugins do.  

Lastly - Animate includes an extensive list of presets, that include the most common animations like hover, pulse, rotate etc. (full list below), that significantly reduce set-up time. Animate is aimed at designers and requires minimal understanding of blueprints. 

<br><be>

## Plug-in Content

<details>

<summary>Animation</summary>

1. Basic
    - Animate (Location) 

    - Animate (Rotation) 

    - Animate (Scale) 

2. Range 

    - AnimateRange (Location) 

    - AnimateRange (Rotation) 

    - AnimateRange (Scale) 

3. Curve

    - AnimateCurve (Location)  

    - AnimateCurve (Rotation)  

    - AnimateCurve (Scale)  

4. Range+Curve 

    - AnimateRangeC(Location) 

    - AnimateRangeC(Rotation) 

    - AnimateRangeC(Scale)

</details>

<details>

<summary>Presets</summary>

- PopIn 

- Hover 

- BounceDown 

- Pulse 

- Roll(Y) 

- Roll(X) 

- RotationLoop 

- MoveTo
  
- PathMove 

- WallBounce

</details>

<details>

<summary>General</summary>

- PauseAnimation 

- UnpauseAnimation 

- StopAnimation 

- IsAnimationActive 
  
</details>


<details>

<summary>Events</summary>

- OnAnimationComplete

</details>

<br><be>

## Set Up

Add the plugin to the “Plugins” folder in your Unreal project’s directory. If there’s no folder under that name in your project files – create a new one. 

After, you can go into your blueprint and in the "Components" window press "Add" and search for **Animation component**. Now, you can use any of the nodes from the list above.

As an example, let’s look at the Animate (Location) node.  <br><br>

<img src="https://github.com/user-attachments/assets/a35aca61-6b18-4f14-b4c1-1a741cb47c28" width="600"> <br><br>

The first input pin ***“Target”*** should be the animation component itself, meanwhile the second  

***“Target Component”*** is the scene component (e.g. static mesh), that you want to animate.  

***“Location”*** refers to the vector amount that is to be added to the scene component’s current location, but if interested in setting both start and end values yourself, use AnimateRange(*Movement Type*).  

***“Duration”*** determines how long the animation will execute in seconds. 

***“Loops”*** is the number of times the animation will execute; 0 for one time, -1 for endless loop.  

***“Yoyo”*** is a type of loop - if false, the loop repeats A->B. If true, the loop alternates A->B and then B->A. 

***“Loop Delay”*** is a length of pause between each loop in seconds. 

***“Ease”*** allows you to choose from 15 included ease types, but if interested in using a custom-made curve float, use AnimationCurve/AnimationRangeC (*Movement Type*). 

***“Transform”*** allows you to choose from 2 transform types. More information under [“World VS Relative Transform”](#world-vs-relative-transform). 

The output pin ***“Handle”*** allows for the use of the General nodes, that require the animation’s timer handle.  

E.g. the Pause Animation node needs a timer handle to pause specific animation.<br><br>

<img src="https://github.com/user-attachments/assets/26210e9e-45fb-4649-96dd-cd0dbfd31b66" width="600"> <br><br>

### The animation nodes work like **latent action nodes** and shouldn't be used with "event tick" or other per-frame updates!

<br><be>

## Important

If an animation is not executing as expected, make sure no other same-movement-type animation is being called at the same time! To prevent unexpected behaviour, if the animation of the same type (location/rotation/scale) is executed when another one is called - the second one WILL NOT execute.  

If the animation behaves weirdly - make sure that the transform you are getting (if using AnimateRange) matches the transform type (world/relative). To see the difference check below! 

If you encounter an unexpected issue, please reach out to describe the problem in detail! 

<br><be>

## Eases

The Animate plugin includes 15 pre-made float curves of 5 distinct types (Sine, Cubic, Back, Elastic and Bounce) that are available with the plugin and each curve can be tweaked to fit the designer's needs better.  <br><br>

<img src="https://github.com/user-attachments/assets/927f6c22-ea2a-4360-967c-812ea8754a80" width="600"> <br><be>

- Sine is more gradual, meanwhile Cubic is more forceful.

<img src="https://github.com/user-attachments/assets/bc7622d5-eeb0-4f64-b443-410597a2b9f4" width="600"> <br><be>

- Back-In slightly goes back before moving to the end position, Back-Out overshoots at the end, and Back-InOut is a combination of them both.
Elastic has a cartoony look and looks most fun with scale animations. <br><be>


<img src="https://github.com/user-attachments/assets/06a22844-b86a-4eca-81da-f56e6d58aea9" width="600"> <br><be>

- Bounces slightly from position.
<br><be>

It's also possible to use custom float curves directly with AnimateCurve or AnimateRangeC nodes.
You can create a custom float curve by going into your content browser -> Add -> Misc -> Curve -> Float. <br><be>

<img src="https://github.com/user-attachments/assets/6262b103-2cdf-4942-a750-5dd3a0c1b34c" width="600"> <br><be>

For the best effect, the curves should go from 0 sec and a value of 0 to 1 sec and a value of 1.

<br><be>

## Presets

The plug-in includes ten presets that reduce setup time and can be plugged in without any additional hassle. <br><be>

As a couple of examples:
<br><be>

![pathmove-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/d5dfc6e4-f30e-42ab-bf43-03c0da1ab5e6) <br><be>

<img src="https://github.com/user-attachments/assets/17791039-5d07-446f-b4d4-78c8e6a4d4db" width="500"> <br><be>

- Path move moves the object through multiple specified points in sequence. <br><be>

<br><be>

![PopIn-ezgif com-video-to-gif-converter (1)](https://github.com/user-attachments/assets/6ffcd220-9b14-4274-b986-26ec9d9d8d16) <br><be>

<img src="https://github.com/user-attachments/assets/56e9ea36-2c49-4c91-b841-7e9e9aa707e6" width="500"> <br><be>

- Pop-In scales the object up from a small size to full size using elastic ease. Works best if the mesh's scale in the viewport is set to 0 (if the start scale is 0). <br><be>

<br><be>

![BounceDown-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/ccd75208-802b-40a3-be36-ead0681373e9) <br><be>

<img src="https://github.com/user-attachments/assets/0eac7bd0-85f3-4fde-bdde-322bc276999b" width="500"> <br><be>

- Bounce Down drops the object to the ground with a bouncing effect. It accounts for the bounds of the mesh, so no additional tweaking should be needed. <br><be>

<br><be>

![wallbounce-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/c1865c08-5537-4e11-ae22-0be9500b848b) <br><be>

<img src="https://github.com/user-attachments/assets/59ba53f2-79d2-4738-9588-b9a01edfafbb" width="500"> <br><be>

- Wall Bounce is similar to Bounce Down. However, it bounces at the side and the direction for the movement can be set.





<br><be>

## World VS Relative Transform

World Transform moves or rotates the object based on the global scene coordinates (the world). Use World Transform when you want the object to move or rotate to a specific position in the world. It ignores the object’s parent and works in the global coordinate space. 

Relative Transform moves or rotates the object based on its parent’s position and orientation. The object will move relative to where its parent is located or how it’s rotated. If there’s no parent, it acts like World Transform.  

Use Relative Transform when you want the object to move or rotate in relation to its parent. This is helpful when animating objects attached to something else (like a door attached to a hinge). 

