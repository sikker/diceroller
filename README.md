DiceRoll
====================================
A simple dice rolling lib for Node or the browser, written in Coffee, distributed as compiled JS.

Usage
-----------------
Clone this repo or install hrough npm:
```
npm install diceroll
```
Include the library client side:
```html
<script src="node_modules/diceroll/diceroll.min.js"></script>
```
Or server side in Node:
```javascript
var diceroll = require("diceroll");
```

Require the function and do a roll:
```javascript
var roll = diceroll({ dice: 2, sides: 20 });
console.log(roll);
```

The roll results in a json object with the following:
```javascript
{
  rolls: [ 17, 5 ],
  conclusion: 22
}
```

'rolls' contains the result of each die roll, conclusion contains the total result. By default the conclusion is the sum of the rolls, but this can be configured.

The following parameters are currently supported:
 - dice [number] (mandatory): the amount of dice to roll
 - sides [number] (mandatory): how many sides each die should have
 - sum [bool]: Whether the conclusion should summarize the rolls or not
 - target [number]: If sum is false, the conclusion will instead contain the amount of rolls that reach or exceed this target number. If, however, sum is true *and* target number is set, the conclusion will contain a boolean true or false depending on whether or not the target number was met.
 - onesSubtract [bool]: If sum is false, any 1s rolled will subtract from the conclusion, possibly making it negative.
 - explodeOn [number]: If sum is false, an extra die will be rolled anytime a die hits or exceeds this number.
 - modifier [number]: Negative or positive number to subtract from or add to the sum conclusion. Has no effect on sum:false rolls.

Example using a target number (6, as is the case in the Vampire: the Masquerade RPG for instance):
```javascript
var roll = diceroll({ dice: 5, sides: 10, sum: false, target: 6, onesSubtract: true });
console.log(roll);
```
The result yielded could look like this:
```javascript
{
  rolls: [3, 10, 4, 2, 8],
  conclusion: 2
}
```
Example using a target number on a summarized roll (such as a D&D d20 roll):
```javascript
var roll = diceroll({ dice: 1, sides: 20, target: 12 });
console.log(roll);
```
The result yielded could look like this:
```javascript
{
  rolls: [ 9 ],
  conclusion: false
}
```
You can roll multiple dice types in the same diceroll. This creates nested diceroll instances that sum their conclusions together and returns their rolls in an array of arrays. Note that if you use a target number with sum:true, the boolean conclusion will be skipped. With sum:false the number of successful target hits gets added to the conclusion (rather than the sum of the rolls). 

Example using multiple dice in the same roll:
```javascript
var roll = diceroll([ { dice: 1, sides: 6 }, { dice: 2, sides: 4, modifier: 1 } ]);
console.log(roll);
```
The result yielded could look like this:
```javascript
{
  rolls: [ [ 3 ], [ 1, 4 ] ],
  conclusion: 9 // sum of the rolls is 8, modifier to the last roll is 1, for a total of 9
}
```

If you wish to run the unit tests for diceroll, enter the module directory and run:
```
npm test
```

Contribution
-----------------------
The licence for this software is found in LICENCE.txt. Pull requests and issues are always welcome.
