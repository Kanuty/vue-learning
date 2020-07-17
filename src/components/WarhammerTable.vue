<template>
  <div class='hello'>
  <label for='race'>Choose a race:</label>
  <select name='race' v-model='selectedRace'>
    <option v-for='race in races' :key=race.name>
      {{ race.name }}
    </option>
  </select>

  <span>selected race: {{selectedRace}}</span>
  <table>
    <tr>
      <th>WW</th>
      <th>US</th>
      <th>K</th>
      <th>Odp</th>
      <th>Zr</th>
      <th>Int</th>
      <th>SW</th>
      <th>Ogd</th>
    </tr>
    <tr>
      <td>{{ weaponSkill }}</td>
      <td>{{ balisticSkill }}</td>
      <td>{{ sturdiness }}</td>
      <td>{{ resistance }}</td>
      <td>{{ agility }}</td>
      <td>{{ inteligence }}</td>
      <td>{{ willPower }}</td>
      <td>{{ fellowship }}</td>
    </tr>
    <tr>
      <th>A</th>
      <th>Żyw</th>
      <th>S</th>
      <th>Wt</th>
      <th>Sz</th>
      <th>Mag</th>
      <th>PO</th>
      <th>PP</th>
    </tr>
    <tr>
      <td>{{ attacks }}</td>
      <td>{{ health }}</td>
      <td>{{ strength }}</td>
      <td>{{ toughness }}</td>
      <td>{{ speed }}</td>
      <td>{{ magic }}</td>
      <td>{{ sanity }}</td>
      <td>{{ destiny }}</td>
    </tr>
  </table>
  </div>
</template>

<script>
const blank = '-'
let race = 'human'

const rollDice10 = (rolls = 1) => {
  let results = 0
  for (let counter = 0; counter < rolls; counter += 1) {
    results += Math.ceil(Math.random() * (10))
  }
  return results
}

const raceBase = {
  human: {
    name: 'human',
    weaponSkill: 20,
    balisticSkill: 20,
    sturdiness: 20,
    resistance: 20,
    agility: 20,
    inteligence: 20,
    willPower: 20,
    fellowship: 20
  },
  elf: {
    name: 'elf',
    weaponSkill: 20,
    balisticSkill: 30,
    sturdiness: 20,
    resistance: 20,
    agility: 30,
    inteligence: 20,
    willPower: 20,
    fellowship: 20
  },
  goblin: {
    name: 'goblin',
    weaponSkill: 15,
    balisticSkill: 20,
    sturdiness: 20,
    resistance: 20,
    agility: 15,
    inteligence: 15,
    willPower: 20,
    fellowship: 10
  },
  orc: {
    name: 'orc',
    weaponSkill: 25,
    balisticSkill: 25,
    sturdiness: 25,
    resistance: 35,
    agility: 15,
    inteligence: 15,
    willPower: 20,
    fellowship: 10
  }
}
const primaryStatistics = {
  weaponSkill: raceBase[race].weaponSkill + rollDice10(2),
  balisticSkill: raceBase[race].balisticSkill + rollDice10(2),
  sturdiness: raceBase[race].sturdiness + rollDice10(2),
  resistance: raceBase[race].resistance + rollDice10(2),
  agility: raceBase[race].agility + rollDice10(2),
  inteligence: raceBase[race].inteligence + rollDice10(2),
  willPower: raceBase[race].willPower + rollDice10(2),
  fellowship: raceBase[race].fellowship + rollDice10(2)
}
const secondaryStatistics = {
  attacks: 1 || blank,
  health: 10 || blank,
  strength: (sturdiness) => Math.floor(sturdiness / 10) || blank,
  toughness: (resistance) => Math.floor(resistance / 10) || blank,
  speed: 4 || blank,
  magic: 0 || blank,
  sanity: 0 || blank,
  destiny: 1 || blank
}

export default {
  name: 'WarhammerTable',
  data () {
    return {
      weaponSkill: primaryStatistics.weaponSkill,
      balisticSkill: primaryStatistics.balisticSkill,
      sturdiness: primaryStatistics.sturdiness,
      resistance: primaryStatistics.resistance,
      agility: primaryStatistics.agility,
      inteligence: primaryStatistics.inteligence,
      willPower: primaryStatistics.willPower,
      fellowship: primaryStatistics.fellowship,

      attacks: secondaryStatistics.attacks,
      health: secondaryStatistics.health,
      strength: secondaryStatistics.strength(primaryStatistics.sturdiness),
      toughness: secondaryStatistics.toughness(primaryStatistics.resistance),
      speed: secondaryStatistics.speed,
      magic: secondaryStatistics.magic,
      sanity: secondaryStatistics.sanity,
      destiny: secondaryStatistics.destiny,

      selectedRace: 'human',
      races: raceBase
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>
