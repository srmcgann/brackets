<template>
  <table>
    <tr>
      <td class="topLeft">
        <LeftCluster
          :indices="[indices[0], indices[1], indices[2], indices[3]]"
          :playerSelectionIndices="[playerSelectionIndices[0], playerSelectionIndices[1]]"
          :playerSelectionIndex="playerSuperIndices[0]"
          :authorMode="authorMode"
          :teams="teams"
          :authSelections="authSelections"
          :playerSelections="playerSelections"
        />
      </td>
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
    </tr>
    <tr>
      <td class="bottomLeft">
        <LeftCluster
          :indices="[indices[4], indices[5], indices[6], indices[7]]"
          :playerSelectionIndices="[playerSelectionIndices[2], playerSelectionIndices[3]]"
          :playerSelectionIndex="playerSuperIndices[1]"
          :authorMode="authorMode"
          :teams="teams"
          :authSelections="authSelections"
          :playerSelections="playerSelections"
        />
      </td>
      <td></td>
    </tr>
  </table>
</template>

<script>
import AuthTeamSelect from '@/components/AuthTeamSelect'
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
import LeftCluster from '@/components/LeftCluster'
export default {
  name: 'LeftSuperCluster',
  components: {
    PlayerTeamSelect,
    AuthTeamSelect,
    LeftCluster
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
