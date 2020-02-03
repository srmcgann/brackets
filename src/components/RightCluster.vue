<template>
  <table>
    <tr>
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

      <td class="topRight">
        <RightNode
          :indices="[indices[0], indices[1]]"
          :playerSelectionIndex="playerSelectionIndices[0]"
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
        <RightNode
          :indices="[indices[2], indices[3]]"
          :playerSelectionIndex="playerSelectionIndices[1]"
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
import AuthTeamSelect from '@/components/AuthTeamSelect'
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
import RightNode from '@/components/RightNode'
export default {
  name: 'RightCluster',
  components: {
    PlayerTeamSelect,
    AuthTeamSelect,
    RightNode
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
