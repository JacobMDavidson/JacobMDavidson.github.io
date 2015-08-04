---
layout: post
title: Ant Simulator
description: "In one of the first classes I took at UIS, CSC 385: Data Structures & Algorithms, the semester project required the development of an ant colony simulation in Java. For the sake of future students taking that course, I will not be revealing the source code or my methods for implementing the project in this summary."
modified: 2015-08-04
tags: [desktop, java]
comments: false
image:
  feature: desktop/ant-simulator.png
---

## Project Summary

In one of the first classes I took at UIS, CSC 385: Data Structures & Algorithms, the semester project required the development of an ant colony simulation in Java. For the sake of future students taking that course, I will not be revealing the source code or my methods for implementing the project in this summary.

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/ant-colony.png" alt="">
</figure>

#### The Environment

The environment is composed of a 27 x 27 square grid, each square of which represents a distinct location. The center square of this grid represents the entrance to the colony. Eight directions of movement are possible from each square, and each square can contain zero or more of the following items:

1. Enemy ants
2. Friendly ants
3. Units of food
4. Units of pheromone

Initially, the center of the square and the immediately surrounding squares are revealed, but the rest are hidden as unexplored terrain. Only scout ants can move into hidden squares. All other types of friendly ants can only move into terrain previously revealed by the scout ants. The simulation runs at the rate of 10 turns per day.

#### The Ants

<u>Queen</u>

The queen ant is indicated by the yellow ant icon in the center square. She has a maximum life span of 20 years and never moves from the center square. The queen hatches new ants at the rate of 1 per day (1 every 10 turns) with the following probabilities for the ant type:

1. Forager - 50%
2. Scout - 10%
3. Soldier - 40%

She consumes 1 unit of food from her square for every turn, and if the food reaches 0, she dies of starvation. The queen can also die from a Bala attack. The simulation immediately ends when the queen dies.

<u>Forager</u>

The green forager ant has a life span of 1 year, and can only move into squares revealed by a scout ant. This ant has two primary modes of behavior, foraging mode and return-to-nest mode. When foraging, this ant moves to the adjacent square with the most pheromones. If more than one square has the same level, the ant randomly chooses the next square to move to. When the forager enters a square with food, it picks up one unit and enters return-to-nest mode.

In return-to-nest mode, the forager follows its exact path back to the nest dropping 10 units of pheromone in each square it travels through. When the forager reaches the nest, it drops the food and returns to foraging mode. If the forager dies while carrying food, the food stays in the square in which the forager died.

<u>Scout</u>

The blue scout ant has a life span of 1 year, and is responsible for enlarging the foraging area. The scout randomly moves to one of the 8 adjacent squares, revealing that square if it is hidden. There's a 25% chance each revealed square will contain a random amount of food between 500 and 1000 units. Once a square is revealed, all other friendly ants are capable of entering that square.

<u>Soldier</u>

The black soldier ants have a life span of 1 year, and are responsible for protecting the colony from enemy bala ants. This ant has two modes, scout mode and attack mode. In scout mode, the soldier moves randomly if there are no bala ants in adjacent squares. If there are bala ants in one or more adjacent squares, the soldier randomly moves to one of the squares with a bala ant, and enters attack mode.

In attack mode, the soldier attacks a specific bala ant within its sqaure. If there are more than one bala ants, the soldier randomly chooses one to attack. During the attack, there is a 50% chance the soldier kills the bala ant.

<u>Bala</u>

The red bala ants are enemies to the colony, and have a life span of 1 year. These ants enter at the periphery of the environment, and have a 3% chance of showing up on each turn. Once it appears, it remains in the environment until it dies from old age or a soldier attack. This ant always moves randomly. If it is in a square with friendly ants, it randomly picks one to attack. During the attack, there is a 50% chance the bala ant kills the friendly ant.

#### The GUI

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/ant-start-screen.png" alt="">
</figure>

The GUI was developed and provided by the professor. The challenge was to analyze the GUI code, and design the simulation to use it. The simulation has five setup options and three controls. The setup options include:

1. Normal setup - Simulation begins with the queen ant, 10 soldier ants, 50 forager ants, 4 scout ants, and 1000 units of food in the center square.
2. Queen test - Tests the queen functionality. Includes the queen ant, with hatching ability enabled, and 1000 units of food. The bala ants are disabled.
3. Scout test - Tests the scout's functionality. Includes the queen ant with hatching disabled, and a single scout ant. The bala ants are disabled.
4. Forage test - Tests the forage ant's functionality. Includes the queen ant with hatching disabled, and 2 forager ants. Bala ants are disabled.
5. Soldier test - Tests the soldier ant's functionality. Includes the queen with hatching disabled, 4 soldier ants, and 4 bala ants. Bala ant generation is disabled.

The control options include:

1. Run - continuously runs the simulation updating the GUI after each turn.
2. Step - Steps the simulation one turn at a time.
3. Pause - Pauses the simulation displaying the results of the most resent turn.

#### Emergent Properties

This project highlights the idea of emergent properties, where larger patterns arise through the interactions of smaller entities. Collectively, these simulated ants work together to grow the colony. The foragers could not find adequate food without the scouts expanding the colony, the colony could not survive without the protection of the soldiers, and the colony needs a queen to continue to grow. The greatest emergent property example from this project is the forager ants ability to hone in on a food source. When the simulation starts, the foragers are randomly searching for food, and display a scattered pattern from the center of the colony:

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/scattered-ants.png" alt="">
</figure>

Soon, some foragers find food and leave a strong pheromone trail that attracts the rest of the foragers. Before long, the foragers will converge on a direct path between the food source and the center of the colony:

<figure style="text-align: center">
    <img src="{{ site.url }}/images/desktop/organized-foragers.png" alt="">
</figure>

This behavior is similar to real life colonies. For example, if you find ants in your kitchen, but don't know where they're coming from, leaving out a food source will reveal the origin. The ants will soon form a line from the food source to wherever it is they're coming from.

## Summary

The learning experience provided by this project was two-fold:

1. I had to quickly become acquainted with another person's code to effectively incorporate the GUI.
2. I had to make heavy use of data structures to optimize the performance of the simulation, which had to calculate the actions of hundreds of ants over thousands of turns.

This project represents one of the most fulfilling experiences during my time at UIS. It was a well designed exercise that greatly increased my programming confidence.
