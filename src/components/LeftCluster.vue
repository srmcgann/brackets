<template>
  <table>
    <tr>
      <td class="topLeft">
        <LeftNode
          :indices="[indices[0], indices[1]]"
          :playerSelectionIndex="playerSelectionIndices[0]"
          :authorMode="authorMode"
          :teams="teams"
          :authSelections="authSelections"
          :playerSelections="playerSelections"
        />
      </td>
      <td class="intermediaryTD">
        <div v-if="!authorMode" class="floatingPlayerSelect">
          <PlayerTeamSelect
            :teamsThisMatch="getSubMatch(playerSelectionIndices[0], playerSelectionIndices[1])"
            :teams="teams"
            :playerSelectionID="playerSelectionIndex"
            :playerSelections="playerSelections"
          />
        </div>
      </td>
    </tr>
    <tr>
      <td class="bottomLeft">
        <LeftNode
          :indices="[indices[2], indices[3]]"
          :playerSelectionIndex="playerSelectionIndices[1]"
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
import LeftNode from '@/components/LeftNode'
export default {
  name: 'LeftCluster',
  components: {
    PlayerTeamSelect,
    AuthTeamSelect,
    LeftNode
  },
  props: [
    'playerSelectionIndex',
    'playerSelectionIndices',
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
