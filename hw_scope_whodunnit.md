#### Episode 1

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Library',
  weapon: 'Rope'
};

const declareMurderer = function() {
  return `The murderer is ${scenario.murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```

**Answer:**
Miss Scarlet

---
#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}


changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
**Answer:**
`verdict`:*Professor Plum*. Can't reassign to const variable in `changeMurderer()` 
(I got this wrong initially - forgot about the const)
---
#### Episode 3

```js
let murderer = 'Professor Plum';

const declareMurderer = function() {
  let murderer = 'Mrs. Peacock';
  return `The murderer is ${murderer}.`;
}

const firstVerdict = declareMurderer();
console.log('First Verdict: ', firstVerdict);

const secondVerdict = `The murderer is ${murderer}.`;
console.log('Second Verdict: ', secondVerdict);
```
**Answer:**
`firstVerdict`: *Mrs. Peacock*. Local `declareMurderer` hides the outer `murderer` scope inside the function block.
`secondVerdict`: *Professor Plum*. Outer block scope of `murderer` variable on line 44 still visible here.
---
#### Episode 4

```js
let suspectOne = 'Miss Scarlet';
let suspectTwo = 'Professor Plum';
let suspectThree = 'Mrs. Peacock';

const declareAllSuspects = function() {
  let suspectThree = 'Colonel Mustard';
  return `The suspects are ${suspectOne}, ${suspectTwo}, ${suspectThree}.`;
}

const suspects = declareAllSuspects();
console.log(suspects);
console.log(`Suspect three is ${suspectThree}.`);
```
**Answer:**
`console.log(suspects)`: *Miss Scarlet, Professor Plum, Colonel Mustard*. Local `suspectThree` hides outer `suspectThree` scope.
`console.log(`Suspect three is ${suspectThree}.`)`: *Mrs. Peacock*. Outer `suspectThree` scope still applies.
---
#### Episode 5

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Kitchen',
  weapon: 'Candle Stick'
};

const changeWeapon = function(newWeapon) {
  scenario.weapon = newWeapon;
}

const declareWeapon = function() {
  return `The weapon is the ${scenario.weapon}.`;
}

changeWeapon('Revolver');
const verdict = declareWeapon();
console.log(verdict);
```
**Answer:**
`console.log(verdict)`: *Revolver*. `const` does not prevent changing an object's values.
---
#### Episode 6

```js
let murderer = 'Colonel Mustard';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    murderer = 'Mrs. White';
  }

  plotTwist();
}

const declareMurderer = function () {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
**Answer:**
`console.log(verdict)`: *Mrs. White*. `plotTwist()` changes `murderer` to Mrs. White within the `changeMurderer` scope.
---
#### Episode 7

```js
let murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    let murderer = 'Colonel Mustard';

    const unexpectedOutcome = function() {
      murderer = 'Miss Scarlet';
    }

    unexpectedOutcome();
  }

  plotTwist();
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
**Answer:**
`console.log(verdict)`: *Mr. Green*. `unexpectedOutcome()` only changes `murderer` in the `plotTwist()`, and not anywhere else, because `plotTwist()` declared a new local `murderer` variable that hides the outer one.
---
#### Episode 8

```js
const scenario = {
  murderer: 'Mrs. Peacock',
  room: 'Conservatory',
  weapon: 'Lead Pipe'
};

const changeScenario = function() {
  scenario.murderer = 'Mrs. Peacock';
  scenario.room = 'Dining Room';

  const plotTwist = function(room) {
    if (scenario.room === room) {
      scenario.murderer = 'Colonel Mustard';
    }

    const unexpectedOutcome = function(murderer) {
      if (scenario.murderer === murderer) {
        scenario.weapon = 'Candle Stick';
      }
    }

    unexpectedOutcome('Colonel Mustard');
  }

  plotTwist('Dining Room');
}

const declareWeapon = function() {
  return `The weapon is ${scenario.weapon}.`
}

changeScenario();
const verdict = declareWeapon();
console.log(verdict);
```
**Answer:**
`console.log(verdict)`: *Candle stick*. Within the `changeScenario()` scope, the room is 'Dining Room', which changes the murderer to 'Colonel Mustard' inside the `plotTwist()` scope, which in turn changes the weapon to 'Candle stick' in `unexpectedOutcome()`.
---
#### Episode 9

```js
let murderer = 'Professor Plum';

if (murderer === 'Professor Plum') {
  let murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```
**Answer:**
`console.log(verdict)`: *Professor Plum*. The if block just declares a new local variable with the same name as the outer variable, and has no effect on 'Professor Plum'.
---

