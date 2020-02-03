<template>
  <table>
    <tr><td class="heightAdjusted"></td></tr>
    <tr>
      <td class="intermediaryTD">
        <div v-if="!authorMode" class="floatingPlayerSelect">
          <PlayerTeamSelect
            :teamsThisMatch="getSubMatch(indices[0], indices[1])"
            :teams="teams"
            :playerSelectionID="98"
            :playerSelections="playerSelections"
          />
        </div>
      </td>
    </tr>
    <tr>
      <td>NFL PLAYOFFS</td>
    </tr>
    <tr><td></td></tr>
  </table>
</template>

<script>
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
export default {
  name: 'PlayoffNode',
  components: {
    PlayerTeamSelect
  },
  props: [
    'indices',
    'authorMode',
    'teams',
    'playerSelections'
  ],
  methods: {
    getSubMatch (A, B) {
      return [
        {name: this.teams[this.playerSelections[A]].name},
        {name: this.teams[this.playerSelections[B]].name}
      ]
    }
  }
}
</script>

<style scoped>
.heightAdjusted{
  height: 84px;
}
</style>
