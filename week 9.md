# Week 9

### Fix Rope Swing
To fix the rope swing mechanic, I decided to make it a scripted swing that only requires the player to press E once and not hold it, that way the swings would be the exact same angle every time, and would be easier to pull off.

<iframe src="https://blueprintue.com/render/9mcuie7p/" scrolling="no" allowfullscreen></iframe>

### Homing Attack
I wanted to give the slimeball a dash attack that made them dash towards nearby enemies.

I first created a script that looked for the nearest enemy closest to the player. It would get every actor with the blueprint interface, and decide if each one was closer than the previous. The first one was compared to a distance of 1000, since I wanted the homing attack to be close range.

<iframe src="https://blueprintue.com/render/f7h96apf/" scrolling="no" allowfullscreen></iframe>

I then wanted to create a search to see if the actor was on-screen. So I used the "convert world location to screen location" node, and, comparing it to the viewport size, check if the actor's screen location was actually on the screen. If not, then it wasn't registered as a valid actor to homing attack.

<iframe src="https://blueprintue.com/render/u2gqvaeb/" scrolling="no" allowfullscreen></iframe>

After successfully finding the target actor, it then simply launches the character towards the target actor.

<iframe src="https://blueprintue.com/render/_rxl-ftn/" scrolling="no" allowfullscreen></iframe>