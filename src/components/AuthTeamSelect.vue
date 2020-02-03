<template>
  <div class="teamSelect">
    <select v-model="teamSelection">
      <option v-for="(team, idx) in teams" :key="idx" v-if="team.name !== null">
        {{team.name}}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'AuthTeamSelect',
  props: ['teams', 'authSelections', 'authID'],
  data () {
    return {
      teamSelection: this.teams[this.authSelections[this.authID]].name
    }
  },
  watch: {
    teamSelection (val) {
      this.$set(this.authSelections, this.authID, this.teams.findIndex(e => e.name === val))
    }
  }
}
</script>

<style scoped>
select{
  background: #4cf;
  font-size: 14px;
  color: #112;
  border: none;
  border-radius: 5px;
  font-family: arial, tahoma;
  font-weight: 700;
  border: 1px solid white;
}
.teamSelect{
  margin-bottom: 40px;
}
</style>
