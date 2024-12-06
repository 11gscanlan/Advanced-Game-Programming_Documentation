# Week 3

## New Power Beam Model
I wanted to create a new arm cannon model, so using the metroid prime arm cannon as a reference, I... bascially just recreated it in Maya.

I'll be brief for this since it was a rather unnecessary side task to acomplish and I really should've been focused on the mechanics, but creating the mesh allowed me to try out animation blueprint states on the mesh.

![](Images/IMG_PrimeCannon_1.png)

![](Images/IMG_PrimeCannon_2.png)

![](Images/IMG_PrimeCannon_3.png)

![](Images/IMG_PrimeCannon_4.png)

![](Images/IMG_PrimeCannon_5.png)

For the animation blueprint, I created switches between 4 different states, which mostly just boiled down to several "Is arm cannon state = 1" flags. So, for example, if the arm cannon state was set to the Wave Beam, aka State 2, then it would switch to the wave beam state.

![](Images/IMG_PrimeCannon_AnimBP.png)



## New Beam VFX
With the new arm cannon, I changed the VFX for the arm cannon, including adding a muzzle flash effect.

[Video Demonstration of Arm Cannon and New Beam VFX](https://youtu.be/ZAQUvjmRYOM)

## Morph Ball

For the morph ball, I created two different functions, one which could be used to toggle the morph ball physics, shrink the player's size and make the camera go third person;

<iframe src="https://blueprintue.com/render/do_n9stf/" scrolling="no" allowfullscreen></iframe>

And another node specifically when attempting to exit the morph ball which would box trace above the player to see if they were in an enclosed place, and prevent the player from exiting the morph ball if they were.

<iframe src="https://blueprintue.com/render/7owpqxgy/" scrolling="no" allowfullscreen></iframe>

## Morph Ball Tunnels

To create tunnels that the player can move through, I created a spline mesh

## Targeting System