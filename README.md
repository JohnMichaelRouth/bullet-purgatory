# bullet-purgatory

simple top down shooter 

Note: This specification document is written in phenotypic descriptions of the output -- descriptions of the behavior of elements of the game, regardless of implementation (whenever possible).

I.E. "Player character's movement triggered by player input."

rather than

"Player character controller must have a functioning movement script with active keypress input listeners."

Furthermore, some items among milestone specifications may not directly correspond to intended behavior for that deliverable -- however, it is intended to provide context of future deliverables as it may inform the chosen method of implementation.

## Definitions

- PC = Player Character
- PC1, PC2, PC3 = First/Second/Third selectable Player Character
- Basic Attack = The attack performed continuously by the PC without requiring player input
- Class = selectable PC option

# Milestone 1 Specifications

### Player Character

- Players will be able to edit keybinds in a future milestone
- PC movement triggered by player input (WASD)
    - Framerate independent movement
    - PC1 - No movement acceleration (listed as PC1 because PC2 will have it in Milestone 2)
    - Movement speed will affected by items/upgrades/etc.
    - PC turns to face the direction they are moving (left-front, right-front, left-back, right-back)

- Each class will have 2 basic attacks, each with their own unique attack time coefficient and attack damage coefficient
    - Players can cycle between them via tapping a key, or they can press and hold the same key to switch until release
- Each class will have
- PC has the following attributes:
    - Strength, primarily affecting physical damage
    - Dexterity, primarily affecting attack speed
    - Agility, primarily affecting move speed
    - Inteligence, primarily affecting crit chance and magic damage
    - Luck, primarily affecting the occurence rate of any non-guaranteed effect

- PC also has the following affectable stats:
    - Hitpoints
    - Move Speed
    - Attack Damage
    - Attack Speed
    - Crit Chance
    - Crit Damage
    - Cooldown Recovery Rate
    - Level
    - Experience

- Basic attacks are performed and animated at rates equal to the coefficient of the attack being performed's attack time coefficient

- PC1's Basic Attack 1 hits enemies in a large oval around them, medium speed
    - Attack does damage equal to the product of PC attack damage and the attack's damage coefficient
    - The attack can critically strike, further multiplying damage dealt by crit damage
- PC1's Basic Attack 2 swiftly strikes thrice, hitting enemies in a wide cone in the direction of the cursor relative to the PC
    - PC1 turns to face the direction of the attack regardless of which direction they are moving in
    - Each strike does damage equal to the product of PC attack damage and the attack's damage coefficient
    - The attack can critically strike, further multiplying damage dealt by crit damage

- PC1 has a distinct hurtbox size from PC2 and PC3
- Upon making contact with an enemy, PC takes damage according to the damage value of the enemy, affected by any relevant items/upgrades that PC may have
- If PC hitpoints reach zero, they perform their death animation (in the future, a summary window will appear here, with statistics of the run such as, number of enemies killed, damage dealt, damage taken, etc.)
- When PC experience reaches the amount required for the next level, time stops, a gray semi-transparent overlay covers the game (this will be animated), and upgrade options are presented.
    - Once selected, the game will resume (the receding of the choices and overlay will also be animated)
    - As a placeholder for the amount of total experience required for each level, one could use the Fibonacci Sequence beginning from 5, or simply require a constant 10 xp per level.
- PC automatically collects any dropped gold in a radius around them

### Enemies

- All normal enemies have hitpoints, move speed, a damage value, a gold drop chance, and an experience value
- When PC reduces the hitpoints of an enemy to zero, they perform their death animation and grant their experience value to the player as experience
    - Normal enemies have a chance to drop 1 gold equal to their gold drop chance multiplied by 2 to the power of (their luck stat divided by 7, plus 1)
        - If this chance exceeds 100%, 1 gold always drops, and the excess over 100% is the chance for a second gold to drop
- Unless otherwise indicated, enemies always follow the shortest route to the player
- Enemies spawn in two main ways: over time in the room currently occupied by the PC and in rooms as they are first entered by the PC

### Environment
- Rooms are composed of square tiles on a grid
- Each stage is composed of procedurally selected pre-made rooms
    - In general, rooms other than the starting room should not have only one connection to another room, as this would create a dead end
- The room where the PC begins the stage is Depth 0, any room connected to that room is Depth 1, etc.
- Stage exits are randomly placed within rooms of a certain minimum depth. For instance, a stage may have a minimum depth of 10: this means that the stage exit cannot spawn before depth 10. It does not, however, mean that the exit will necessarily spawn at depth 10.
    - Stage exits have an chance to spawn per room increasing with depth, with a maximum chance of 50%.
    - Stage exits trigger an animation on contact with the PC, and render the PC invulnerable (as the stage is over)
- Treasure chests have a chance to spawn in certain spots in each room, increasing with depth, up to a maximum chance of 7% per room
