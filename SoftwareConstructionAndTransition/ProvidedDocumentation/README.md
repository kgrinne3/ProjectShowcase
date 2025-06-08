# SER316 Fall 2022 B Assignment 5

Katie Grinnell (kgrinne3)

Master [![Gradle Build](https://github.com/kgrinne3/assign5/actions/workflows/gradleBuild.yml/badge.svg?branch=master)](https://github.com/kgrinne3/assign5/actions/workflows/gradleBuild.yml)

Dev [![Gradle Build](https://github.com/kgrinne3/assign5/actions/workflows/gradleBuild.yml/badge.svg?branch=dev)](https://github.com/kgrinne3/assign5/actions/workflows/gradleBuild.yml)

![Coverage](.github/badges/jacoco.svg)

![Branches](.github/badges/branches.svg)

 ---

## [Video](https://youtu.be/NdrwHHNXEO8)
## Patterns Used
 - MonManager is a **_Prototype Factory_** that contains the Code-a-Mons and returns a clone of a random Mon or of a Mon of a specified type. 
   - The type of Code-a-Mon returned (if not specified) is determined at runtime by a call to Math.random.
   - Additionally, the MonManager returns an object of type Mon, thereby allowing manipulations to be implemented without concern for the random implementation.
 - DayState and NightState are the individual **_State_** implementations, and the SimStateManager controls their execution. 
   - Both states implement the same methods and hold all logic that will occur during that specific state. 
   - State transitions are explicit, and only one state can be 'active' at any given time. 
 - AttackControl is the context class for the **_Strategy_**, and each individual attack type is defined within that directory. 
   - The attack type is determined at runtime, the attack control selects the appropriate strategy, and then the attack method is called.
   - By calling the attack method, the attack method of the current strategy is called, which contains the appropriate algorithm for that specific strategy. 

## Requirements Implemented

### Prototype Factory
 - Code-a-Mons will compete 1-v-1 with another trainer's Code-a-Mon.
 - Code-a-Mons should be of different types and gain advantages or disadvantages bases on their opponent's type.
 - Code-a-Mons should have 
   - Attack 
   - Defense
   - Health
   - 2 different attacks
 - Code-A-Mons will gain experience points from winning battles and can level up after earning enough points.
 - When a Code-a-Mon's health reaches zero, they faint. 
 - Experience points are gained by an individual Code-a-Mon during battle.
### State
- Code-a-Mons will compete 1-v-1 with another trainer's Code-a-Mon.
- Simulation should run on cycles. A cycle is considered to be of 2 parts - 1 day and one night. 
- Battles with other trainers (or other Code-a-Mons) are done during the Daytime. 
- During the night, Code-a-Mons can heal.
- Only one battle can occur at a time. A battle is always between two trainers, each using one Code-A-Mon.
- During battles:
   - Each trainer has 1 Code-A-Mon on the field at a time.
   - Attacks should be performed in a turn-based manner.
   - When a Code-A-Mon's health reaches zero, they faint, and this particular fight is over.
   - Code-A-Mons can heal during the night and be awake again the next day.
   - When a trainer has no Code-A-Mons left, they are removed from the battlefield.

### Strategy
- Code-a-Mons will compete 1-v-1 with another trainer's Code-a-Mon.
- Code-a-Mons should be of different types and gain advantages or disadvantages bases on their opponent's type.
- During battles:
  - Each trainer has 1 Code-A-Mon on the field at a time. 
  - Attacks should be performed in a turn-based manner. 
  - When a Code-A-Mon's health reaches zero, they faint, and this particular fight is over. 
  - Code-A-Mons can heal during the night and be awake again the next day. 
  - When a trainer has no Code-A-Mons left, they are removed from the battlefield. 

    

 ---
## SpotBugs
![](screenshots/spotBugsReport.jpg)
Bad Practice Warnings in all six of the mon type classes
- Flagged because `clone()` is defined but the class does not implement `Cloneable`. 
- However, the stated exception is applicable in this case as I wish to control how subclasses can clone themselves. 
- Additionally, implementing `Cloneable` would provide a deep copy of the object, when I only wish for a shallow copy.


## Checkstyle
![](screenshots/checkstyleMain.jpg)
![](screenshots/checkstyleTest.jpg)

## Coverage
![](screenshots/coverageReport.jpg)

## JUnit
![](screenshots/JUnit.jpg)