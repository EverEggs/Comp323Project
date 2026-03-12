# G2 - Game Demo Walkthrough Plan

## 0) Team Details
**Project:** Last Stand  
**Team Name:** Boatmurdered  
**Members:** Michael Barrow, Mitchell Radzienda, Faris Siddiqi  
**Repo:** https://github.com/EverEggs/Comp323Project  
**Build target:** Win11, Python 3.12  

## 1) Demo Goal
TODO: Michael

## 2) Controls and Player Task
TODO: Michael

## 3) Playable Demo Script
### a) Mitchell (architecture and state machine)
TODO: Mitchell
### b) Michael (input and player behavior)
TODO: Michael
### c) Faris (enemy behavior and collision)
Script: 
My main responsibility was the enemy system from how enemies are defined, to how they move, to how they interact with the player.
I started by creating enemies.json, which externalizes all enemy data so new enemy types can be added without touching any Python code. Each entry defines things like speed, health, radius, and a move_style integer that maps to an enum.
In enemy.py, I built out the Enemy class. The __init__ takes a spawn position and a target the player along with keyword arguments for every attribute, all with defaults. This design lets me create an enemy directly from a JSON template. I also wrote three helper functions: load_enemy converts raw JSON values into proper Python types like pygame.Color and the Movement_styles enum, load_enemies reads the whole file and keys each template by name, and spawn_from_template combines them to actually create an Enemy.
For movement, I implemented the chaser behavior in update() it calculates the vector from the enemy to the player, normalizes it to a direction, then multiplies by speed and delta time so movement is frame-rate independent.
On the player side, I added health, max_health, and a damage_cooldown timer that ticks down each frame and grants brief invincibility after a hit.
In game.py, I put everything together. _spawn_enemy randomly picks one of the four playfield edges and spawns a chaser from the loaded template. _check_collisions does circle-vs-circle math between every enemy and the player — using squared distance to avoid a square root — and triggers the cooldown on hit. _check_projectile_collisions does the same for bullets against enemies, dealing 4 damage per hit, consuming the bullet, and awarding score when an enemy dies.

Press/Click/Type: 
- Show the enemies spawning by starting the game -> enemies should spawn from different sides of the map one at a time 
- When talking about collision show what happens when shooting the enemies by left-clicking the mouse -> response the enemy dies after 3 hits 
- Then show player enemey collisions by standing still and letting the enemies kill the player -> player should die and the gameover screen should display 
## 4) Architecture Map
TODO: Mitchell

## 5) Reliability Checklist
- Pull any new changes and confirm the game launches without issue 
- Confirm documentation/instructions is up to date 
- Test player movements, make sure all movement key are functions 
- Test the shooting, make sure bullets are being fired and are colliding with the enemies 
- Confirm once all enemies die we see the next wave screen/win screen 
- Make sure enemies + player collisions is functioning. 
- Confirm arena bounds are set correctly 

## 6) Playtest and Feedback Plan
Questions We Want answered:
- Can a first-time player understand the goal and win condition without being told?
- Does the game over / restart flow feel immediate and clear?

Clarity / Readability
- When you took damage, could you tell it happened — did anything on screen make it clear you were hit and briefly invincible?
- After the game ended, did the "Game Over — Press Space" screen tell you everything you needed, or were you unsure what just happened or what to press

Control Feel
- Did the player movement feel responsive? 
- When an enemy touched you, did the damage feel fair, or did hits feel instant and unavoidable because the cooldown window was too short?

State / Scene Coherence
- When you pressed Space on the game over screen, did everything reset cleanly (player position and enemies)? 
- On the title screen, was it immediately clear that Space starts the game and did you understand the goal of the game?

## 7) Contributions
Michael: 1, 2, 3b  
Mitchell: 3a, 4  
Faris: 3c, 5, 6  