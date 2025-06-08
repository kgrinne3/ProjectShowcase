### Plan/Goal:

  ----
Battle Royal Style
- One 'main' trainer against a preset number of opponents in the area
- Player will 'wander' the area, with a 40-50% chance of encountering opponents
- Every encounter will have a 10-15% chance of being a wild code-a-mon
- Both the Player and the opponents may have **up to** 6 code-a-mons
- Player and opponents can only have one code-a-mon active at a time (`Singleton?`)

Acquiring Code-a-mons
- Wild Code-a-mons can be encountered while wandering the area
- When encountered, the Player can either run away, or attempt to catch the code-a-mon
- In order to catch the code-a-mon, the trainer must weaken it to **below 50% HP**
  but **above 25% HP**
- ONLY when HP is in that range will the trainer be allowed to attempt to catch the
  code-a-mon
- If successfully caught, the code-a-mon will remain mad at the trainer for
  **TWO FULL NIGHT CYCLES** and will only become available on the third night.
    - If caught day 7, will be locked day 7, night 7, day 8, night 8, day 9,
      will unlock on night 9, and be available for battle on day 10.
    - When the code-a-mon 'forgives' the trainer on the third night, **all** the code-a-mons
  that belong to that trainer will gain a full level of experience.

Simulation
- Tick based (`Mediator?`)
- Day activities:
    - Fight trainer
    - Weaken and attempt to catch code-a-mon
    - Run Away from trainer or code-a-mon
- Night activities:
    - ALL Code-a-mons regenerate health (start each day with 100% HP)
    - Acquired Code-a-mons can unlock during this time
    - Stores are open

Player
- Both the main Player and the opponents are 'Player' class objects
- Trainers do not have health
- Trainers do not take damage
- Trainers can earn and spend money
- Trainers must have a code-a-mon equipped at all times
- If the equipped code-a-mon faints, it is replaced by the next available code-a-mon
- Trainers unable to equip a code-a-mon will be removed from the battle arena
- Trainers can have a maximum of six code-a-mons in their possession at any one time

Code-a-mon (`Abstract Factory`)
- Element Type (`Factory`)
    - Water => weak vs: ice // strong vs: rock
    - Ice => weak vs: fire // strong vs: water
    - Fire => weak vs: wind // strong vs: ice
    - Rock => weak vs: water // strong vs: radiation
    - Wind => weak vs: radiation // strong vs: fire
    - Radiation => weak vs: rock // strong vs: wind
- Experience points
- Level
- XP per level
- Levels per Evolution
- Health
- Attack
- Defense
- Each Code-a-mon will have **at least two** different attacks (`Chain of Responsibility?`)
- If Health reaches zero, the code-a-mon will faint for the rest of the day




 ----
IF TIME PERMITS:
- Trainers carry items
- Code-a-mons can **eat food** and **wear clothing**
- Stores sell the following:
    - Food (_Health Gain_)
        - snack => gain 50% of total
        - meal => gain 75% of total
        - **thinking one item per code-a-mon battle (max 6 per attack sequence)
    - Clothing (_Damage Reduction_)
        - Raincoat => take 50% less dmg from water attacks
        - Sweater => take 50% less dmg from ice attacks
        - Fireman's gear => take 50% less dmg from fire/lava attacks
        - Climbing gear => take 50% less dmg from earth/rock attacks
        - Skydiving wing suit => take 50% less dmg from wind/air attacks
        - Hazmat suit => take 50% less dmg from radiation attacks
        - **thinking length of wear will increase with price
            - cheapest last like 3-5 hits
            - most expensive last several hundred hits
        - **thinking limit to 3 equipment changes per attack sequence
- Trainers can equip clothing on their Code-a-mons that will apply a buff for
  a limited number of hits
- After fainting, code-a-mons will have a **negative attack buffer** for the next full day