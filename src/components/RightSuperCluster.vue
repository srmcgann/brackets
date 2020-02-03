<template>
  <table>
    <tr>
      <td class="intermediaryTD">
        <div v-if="!authorMode" class="floatingPlayerSelect">
          <PlayerTeamSelect
            :teamsThisMatch="getSubMatch(playerSuperIndices[0], playerSuperIndices[1])"
            :teams="teams"
            :playerSelectionID="playerSelectionIndex"
            :playerSelections="playerSelections"
          />
        </div>
      </td>

      <td class="topRight">
        <RightCluster
          :indices="[indices[0], indices[1], indices[2], indices[3]]"
          :playerSelectionIndices="[playerSelectionIndices[0], playerSelectionIndices[1]]"
          :playerSelectionIndex="playerSuperIndices[0]"
          :authorMode="authorMode"
          :teams="teams"
          :authSelections="authSelections"
          :playerSelections="playerSelections"
        />
      </td>
    </tr>
    <tr>
      <td></td>
      <td class="bottomRight">
        <RightCluster
          :indices="[indices[4], indices[5], indices[6], indices[7]]"
          :playerSelectionIndices="[playerSelectionIndices[2], playerSelectionIndices[3]]"
          :playerSelectionIndex="playerSuperIndices[1]"
          :authorMode="authorMode"
          :teams="teams"
          :authSelections="authSelections"
          :playerSelections="playerSelections"
        />
      </td>
    </tr>
  </table>
</template>

<script>
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
import RightCluster from '@/components/RightCluster'
export default {
  name: 'RightSuperCluster',
  components: {
    PlayerTeamSelect,
    RightCluster
  },
  props: [
    'playerSelectionIndex',
    'playerSelectionIndices',
    'playerSuperIndices',
    'indices',
    'authorMode',
    'teams',
    'authSelections',
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
