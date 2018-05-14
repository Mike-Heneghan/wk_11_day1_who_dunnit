# Scope Homework: Who Dunnit

### Learning Objectives

- Understand function scope
- Know the difference between the let and const keywords

## Brief

Using your knowledge about scope and variable declarations in JavaScript, look at the following code snippets and predict what the output or error will be and why.

### MVP

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
Suspicion: Murderer to be stated as Miss Scarlet

Actual: Cracked the Case! The murderer was indeed Miss Scalet.
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
Suspicion: Murderer Professor Plum can't be overwritten as it is a const variable. Therefore Professor Plum is the murderer.

Actual: Cracked the Case! The murderer was indeed Professor Plum.
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
Suspicion: Murderer is initially suspceted to be Professor Plum although the variable is a let. In declareMurderer it is reassigned to be Mrs. Peacock. First verdict should therefore be Mrs. Peackock. The second vedict is called after the murderer has already been set to Mrs. Peacock so she should also be the second verdict?

Actual: Watson is furious, I've failed the case! The first verdict was indeed Mrs. Peacock although the second verdict was Professor Plum. This is as the let function in declare murderer is block scoped and therefore only effects the murderer variable in the declareMurderer function.
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
Suspicion: All three suscpects should be Miss Scarlet, Professor Plum and Colonel Mustard. Although supect three when logged should be Mrs. Peacock as the redefine of suspect three was done inside the declareAllSuspects block.

Actual: Cracked the case! 
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
Suspicion: As the scenario is a const type variable and strings are immutable the murder weapon should not be able to be reassigned to 'Revolver'. Therefore the murder was done by Miss Scarlet, in the Kitchen and with the candle stick.

Actual: Watson is furious again, I've failed another case. As it was the scenario object that was set as a const type variable the attribute of weapon could still be changed. Therefore the weapon was changed to the revolver.
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
Suspicion: The murderer is initially declared outside the function as a let type variable give the value of Colonel Mustard. The change murderer function first changes the murderer to Mr Green and is not type set and therefore global? The plottwist method is then written which changes the murderer to Mrs. White and called. The change murderer method is called then the verdict set as the result of the declareMurderer method. Therefore the killer was Mrs. White?

Actual: Cracked the case!
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
Suspicion: The murderer is set as Professor Plum in a let type variable outside any functions. When changeMurderer is called the murderer is set as Mr Green as a global type variable. Plot twist calls the murderer Colonel Mustard although it is a let type (block scoped) variable. unexpectedOutcome sets the murderer as Miss Scarlet as it is again global. Therefore the murderer was Miss Scarlet.

Actual: Foiled once more! Watson has quit and is off to find a new detective with a stupid name, Sherlock Holmes. I'm going to have to employ Simon as my new biographer. In the plot twist method the block scoped let variable murderer is set as Colonel Mustard. The unexpected outcome resets the variable holding Colonel Mustard not Mr Green.
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
Suspicion: The scenario starts with Mrs Peacock in the conservatory with the Lead Pipe. The change scenario method is called. Murderer becomes Mrs Peacock and rooms becomes dining room. Plot twist is called with Dining Room. Murderer gets changes to Colonel Mustard. Unexpected outcome then called with 'Coloner Mustard'. As the if evaluates to true the murder weapon changes to the 'Candle Stick' The verdict is therefore that the murder weapon was the candle stick.

Actual: Cracked the case!
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
Suspicion: Murderer is a let type variable with Professor Plum. The if case is met but it is redefined only in the block? Therefore it is not changed.

Actual: Cracked the case!
### Extensions

Make up your own episode!
