DiceRoll
====================================
A simple dice rolling lib for Node, written in Coffee.

Usage
-----------------
Clone this repo or install hrough npm:
  npm install diceroll

Require the class and construct a new dice roll:
  var DiceRoll = require("diceroll");
  var roll = new DiceRoll({ dice: 2, sides: 20 });
  console.log(roll.result());

The dice roll results in a json object with the following:
  {
    rolls: [ 17, 5 ],
    conclusion: 22
  }

'rolls' contains the result of each die roll, conclusion contains the total result. By default the conclusion is the sum of the roll results, but this can be configured.

Note that the roll is fully initialized upon creation, result merely feeding you the results. Result can as such be called multiple times with the result staying the same. If you want to reroll, make a new DiceRoll.

The following parameters are currently supported:
 - dice [number] (mandatory): the amount of dice to roll
 - sides [number] (mandatory): how many sides the dice should have
 - sum [bool]: Whether the conclusion should summarize the roll results or not
 - target [number]: If sum is false, the conclusion will instead contain the amount of rolls that reach or exceed this target number.

Example using a target number (6, as is the case in the Vampire: the Masquerade RPG for instance):
  var roll = new DiceRoll({ dice: 5, sides: 10, sum: false, target: 6 });
  console.log(roll.result());
The result yielded could look like this:
  {
    rolls: [3, 10, 4, 2, 8],
    conclusion: 2
  }

If you wish to run the unit tests for DiceRoll, do so with
  npm test

Future plans
----------------------
These are features that may or may not make it into the code in the foreseeable future:
 - Exploding dice (dice that reach a certain threshold are re-rolled for additional value)
 - Ones subtract (in certain RPG systems any 1s rolled reduce the conclusion number)
 - Multiple types of dice in the same roll (support for rolling "1d10 + 1d8")
 - Static modifiers (support for rolling "1d6 +2")

Contribution
-----------------------
The licence for this software is found in LICENCE.txt. Pull requests and issues are always welcome.