<template>
  <div class="teamSelect" v-if="teamsThisMatch[0].name !== null && teamsThisMatch[1].name !== null">
    <select v-model="playerSelections[playerSelectionID]">
      <option v-for="(team, idx) in teamsThisMatch" :key="idx" :value="teams.findIndex(e => e.name === team.name)">
        {{team.name}}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'PlayerTeamSelect',
  props: ['teams', 'teamsThisMatch', 'playerSelections', 'playerSelectionID'],
  data () {
    return {
      playerSelection:
        this.playerSelections[this.playerSelectionID]
          ? this.teams[this.playerSelections[this.playerSelectionID]].name : ''
    }
  }
}
</script>

<style scoped>
select{
  background: #4cf;
  font-size: 15px;
  color: #112;
  border: none;
  border-radius: 5px;
  font-family: arial, tahoma;
  font-weight: 700;
  border: 1px solid #fff;
}
.teamSelect{
  margin-bottom: 40px;
}
</style>
