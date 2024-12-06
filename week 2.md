# Week 2


### Arm Cannon mesh

- Model
- UV Unwrapping
- Texturing
- Rigging
- Animations

---

### Power Beam

I created the default fire mode by first creating a modular script that spawned in the projectile I wanted at the end of the arm cannon, which I could then later change to spawn different projectiles once I added the other beams and their charged variants.

<iframe src="https://blueprintue.com/render/o4-w7b1d/" scrolling="no" allowfullscreen></iframe>

---

### Charge Beam
I created the Charge Beam by using a seperate input that used left click assigned to a timeline. I like using timelines for creating systems that need either a short duration of what is essentially "event tick", or a delay that can be interrupted.

In this case I used the latter. Holding down left click would start timeline set to 0.5 seconds which, when finished, would set a variable to true saying that the beam was fully charged. After which, releasing left click would check to see if the flag is true and, if so, fire the charge beam.

<iframe src="https://blueprintue.com/render/tu_jx-2g/" scrolling="no" allowfullscreen></iframe>

---

### Missiles
Creating missiles was as simple as recreating the primary fire script, however I also made an integer variable that tracked the ammo counter, and wouldn't fire if the player was out of missiles.


<iframe src="https://blueprintue.com/render/h5q4xvpo/" scrolling="no" allowfullscreen></iframe>

---

### Switching Beams

I created an enumerator that tracked which beam state the player's arm cannon was in, which would be used at the point of firing the arm cannon to switch which beam to fire.

After that, I created a quick script that changed the beam. It is controlled by hitting the 1,2,3 or 4 keys to execute the 4 different nodes to swap beams.

<iframe src="https://blueprintue.com/render/p0tb1egw/" scrolling="no" allowfullscreen></iframe>

---

- Wave Beam
- Ice Beam
- Plasma Beam

### Visor Texture Widget


### Test Area

## Project State Demonstration Video

[Project State Week 2](https://youtu.be/IUVH7G2YVbI)