<template>
  <table>
    <tr>
      <td class="intermediaryTD">
        <div v-if="!authorMode" class="floatingPlayerSelect">
          <PlayerTeamSelect
            :teamsThisMatch="getMatch(indices[0], indices[1])"
            :teams="teams"
            :playerSelectionID="playerSelectionIndex"
            :playerSelections="playerSelections"
          />
        </div>
      </td>

      <td class="topRight">
        <div v-if="authorMode" class="floatingSelect">
          <AuthTeamSelect :teams="teams" :authID="indices[0]" :authSelections="authSelections" />
        </div>
        <div v-else class="floatingSelect">
          {{teams[authSelections[indices[0]]].name}}
        </div>
        <h2>
          <img :src="require('@/assets/logos/' + teams[authSelections[indices[0]]].name + '.png')" class="logo" />
        </h2>
      </td>
    </tr>
    <tr>
      <td></td>
      <td class="bottomRight">
        <div v-if="authorMode" class="floatingSelect">
          <AuthTeamSelect :teams="teams" :authID="indices[1]" :authSelections="authSelections" />
        </div>
        <div v-else class="floatingSelect">
          {{teams[authSelections[indices[1]]].name}}
        </div>
        <h2>
          <img :src="require('@/assets/logos/' + teams[authSelections[indices[1]]].name + '.png')" class="logo" />
        </h2>
      </td>
    </tr>
  </table>
</template>

<script>
import AuthTeamSelect from '@/components/AuthTeamSelect'
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
export default {
  name: 'RightNode',
  components: {
    PlayerTeamSelect,
    AuthTeamSelect
  },
  props: [
    'playerSelectionIndex',
    'indices',
    'authorMode',
    'teams',
    'authSelections',
    'playerSelections'
  ],
  methods: {
    getMatch (A, B) {
      return [
        {name: this.teams[this.authSelections[A]].name},
        {name: this.teams[this.authSelections[B]].name}
      ]
    }
  }
}
</script>
