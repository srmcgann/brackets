<template>
  <table>
    <tr>
      <td class="topLeft">
        <div v-if="authorMode" class="floatingSelect">
          <AuthTeamSelect :teams="teams" :authID="indices[0]" :authSelections="authSelections" />
        </div>
        <div v-else class="floatingSelect">
          {{teams[authSelections[indices[0]]].name}}
        </div>
        <h1>
          <img :src="require('@/assets/logos/' + teams[authSelections[indices[0]]].name + '.png')" class="logo" />
        </h1>
      </td>
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
    </tr>
    <tr>
      <td class="bottomLeft">
        <div v-if="authorMode" class="floatingSelect">
          <AuthTeamSelect :teams="teams" :authID="indices[1]" :authSelections="authSelections" />
        </div>
        <div v-else class="floatingSelect">
          {{teams[authSelections[indices[1]]].name}}
        </div>
        <h1>
          <img :src="require('@/assets/logos/' + teams[authSelections[indices[1]]].name + '.png')" class="logo" />
        </h1>
      </td>
      <td></td>
    </tr>
  </table>
</template>

<script>
import AuthTeamSelect from '@/components/AuthTeamSelect'
import PlayerTeamSelect from '@/components/PlayerTeamSelect'
export default {
  name: 'LeftNode',
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
  },
  mounted () {
    this.indices[0] = 0
    this.indices[1] = 0
  }
}
</script>
