---
title: Use .map(), .reduce(), and .filter()
sidebar: mydoc_sidebar
permalink: javascript_map_reduce_filter.html
folder: javascript
---
## .map()

Return an array containing only the id of each person

```javascript
// What you have
const officers = [
  { id: 20, name: 'Captain Piett' },
  { id: 24, name: 'General Veers' },
  { id: 56, name: 'Admiral Ozzel' },
  { id: 88, name: 'Commander Jerjerrod' }
];
// What you need
[20, 24, 56, 88]
```

```javascript
const officerIds = officers.map(officer => officer.id)
```

## .reduce()

Only diffence is that reduce passes the result of this callbak (the accumulator) from one array element to the other.

Return the total years of experience of all of them.

```javascript
const pilots = [
  {
    id: 10,
    name: "Poe Dameron",
    years: 14,
  },
  {
    id: 2,
    name: "Temmin 'Snap' Wexley",
    years: 30,
  },
  {
    id: 41,
    name: "Tallissan Lintra",
    years: 16,
  },
  {
    id: 99,
    name: "Ello Asty",
    years: 22,
  }
]
```

```javascript
const pilotsYears = pilots.reduce((acc, pilot) => acc + pilot.years, 0)
```

## .filter()

filter is used when there is an array but only want some of the elements in it.

Return two arrays: one for Rebels and the other one for Empire.

```javascript
const pilots = [
  {
    id: 2,
    name: "Wedge Antilles",
    faction: "Rebels",
  },
  {
    id: 8,
    name: "Ciena Ree",
    faction: "Empire",
  },
  {
    id: 40,
    name: "Iden Versio",
    faction: "Empire",
  },
  {
    id: 66,
    name: "Thane Kyrell",
    faction: "Rebels",
  }
];
```
```javascript
const arrRebel = pilots.filter(pilot => pilot.faction === 'Rebels')
const arrEmpire = pilots.filter(pilot => pilot.faction === 'Empire')
```

## Combining .map() .reduce() .filter()

Get the total scores of force users

```javascript
const personnel = [
  {
    id: 5,
    name: "Luke Skywalker",
    pilotingScore: 98,
    shootingScore: 56,
    isForceUser: true,
  },
  {
    id: 82,
    name: "Sabine Wren",
    pilotingScore: 73,
    shootingScore: 99,
    isForceUser: false,
  },
  {
    id: 22,
    name: "Zeb Orellios",
    pilotingScore: 20,
    shootingScore: 59,
    isForceUser: false,
  },
  {
    id: 15,
    name: "Ezra Bridger",
    pilotingScore: 43,
    shootingScore: 67,
    isForceUser: true,
  },
  {
    id: 11,
    name: "Caleb Dume",
    pilotingScore: 71,
    shootingScore: 85,
    isForceUser: true,
  },
]
```

```javascript
  const forceUsersSum = personnel
    .filter(per => per.isForceUser)
    .reduce((acc, per) => acc + per.pilotingScore + per.shootingScore, 0)
```

```javascript
  const forceUsersSum = personnel.reduce((acc, per) => {
    return per.isForceUser ? acc + per.pilotingScore + per.shootingScore : acc
  }, 0)
```

## .some()

Return true or false when one or mor of its values correspond to something you're looking for.
When its value is true then it returns true right away without further checking.

Check if there are any pilots among operatives.

```javascript
const operatives = [
  { id: 12, name: 'Baze Malbus', pilot: false },
  { id: 44, name: 'Bodhi Rook', pilot: true },
  { id: 59, name: 'Chirrut Îmwe', pilot: false },
  { id: 122, name: 'Jyn Erso', pilot: false }
];
```

```javascript
const listHasPilots = operatives.some(operative => operative.pilot)
```

## .every()

Check if every value of the array matches a condition.

Check if all pilots are ture among operatives

```javascript
const listHasPilotsOnly = operatives.every(operative => operative.pilot)
```

## .find()

Find the element and return the first value matching the condition

```javascript
const operatives = [
  { id: 12, name: 'Baze Malbus', pilot: false },
  { id: 44, name: 'Bodhi Rook', pilot: true },
  { id: 59, name: 'Chirrut Îmwe', pilot: false },
  { id: 122, name: 'Jyn Erso', pilot: false }
];
```

```javascript
const firstPilot = operatives.find(operative => operative.pilot)
```