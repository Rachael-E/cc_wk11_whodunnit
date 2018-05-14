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

Answer should be Miss Scarlet.

#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const delcareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```
Answer Professor Plum, because the changeMurderer function is constant, it wouldn't allower murderer to be changed to Mrs PeaCock?

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

First Verdict will be Mrs Peacock, the second verdict will be Professor Plum.

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
declareAllSuspects will be Miss Scarlet, Prof Plum and Cnl Mustard. The first console.log will as in the previous sentence: but the last console.log will print Mrs. Peacock, since it is not referring to declareAllSuspects at this point.

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

in changeWeapon, I don't think it will change to the new weapon, as it is a const. I think that declareWeapon will return Candle Stick. So the log will return Candle Stick. Uh oh...no! It's revolver when running the code. But why? Because weapon within scenario isn't constant: it's global? Ok, will ask about this.

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

Ok, so in changeMurderer, because murderer is let, it can be changed to Mr. Green. Same with in plotTwist: the murderer can be changed to Mrs. White because murderer is a let. When plotTwist is called, Mrs. White is the murderer. declareMurdere, the murderer is Mrs.White. But then it's changed to Mr. Green. So the Murderer is Mr. Green? 

Uh oh, no...it's Mrs. White :( ah ok, because plotTwist is actually part of the changeMurderer method! Oops. Okies.

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

I think Cnl Mustard. Since the outcome of changeMurderer is to call plotTwist, where the murderer is changed to Cnl Mustard. Nooooo. it's Mr Green :((( I don't understand this one. Spoke with Keith: it's because murderer for Mr Green is global, and so that is what the end result returns: it doesn't look for the more local version that is defined by let. 

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

plotTwist: if dining room is passed in, the murderer will be Mustard. then, in unexpected outcome, if Mrs PeaCock is passed in, the weapon becomes a candlestick. If it's anyone else, remains lead pipe. So changeScenario should be returning Mustard and Lead pipe. So i think verdict should be lead pipe. Noooooo. it's the candle stick grrr arrrghh. Yes of course, I get it, because dining room was passed in, then the weapon changed to candlestick. Answer: CandleStick.

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
It's Professor Plum...I thought it was Mrs. Peacock though. Don't really understand why in the if statement, it's found that Professor Plum is the murderer, so it's changing it to Mrs. Peacock, so the murderer should be Peacock!? Need to ask about this one. 

### Extensions

Make up your own episode!
