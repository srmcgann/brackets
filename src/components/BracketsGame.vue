<template>
  <div class="main">
    <div class="header">
      <img src="../assets/dollar.png" class="siteLogo">
      <div class="headerControls" v-if="showAdmin">
        <label for="authorMode">Author Mode </label>
        <input type="checkbox" id="authorMode" v-model="authorMode"><br><br>
        <label for="numContestants">Contestants</label>
        <select id="numContestants" v-model="numContestants">
          <option>4</option>
          <option>8</option>
          <option>16</option>
        </select>
      </div>
    </div>
    <br>
    <div :class="{ cont4, cont8, cont16 }">
      <div v-if="showFinalResults">
        <br><br><br>
        <div class="statusMessage">
          Player Won the Following Picks -<br><br>
        </div>
        <div v-for="(result, idx) in finalResults" :key="idx" class="results">
          {{result}} <br>
        </div>
        <div v-if="finalResults.length === 0" class="results">
          No Games were won in this Bracket
        </div>
        <br><br>
        <button @click="reset()">Start Over</button>
      </div>
      <div v-else>
        <div v-if="picksCompleted" class="picksComplete">
          <div v-if="identifyWinningBracket">
            <img src="@/assets/identifyButton.png" @click="checkPicks()" class="picksCompleteButton" />
          </div>
          <div v-else>
            PICKS COMPLETE!
            <img src="@/assets/button.png" @click="submitPicks()" class="picksCompleteButton" />
          </div>
         <br>
        </div>
        <div v-else-if="identifyWinningBracket" class="statusMessage">
          <br><br>
          Game Master: Identify Winning Bracket...
        </div>
        <div v-else>
          <div v-if="authorMode" class="statusMessage">
            CHOOSE CONTESTANTS
          </div>
          <div v-else class="statusMessage">
            PLACE YOUR BETS!
          </div>
        </div>
      </div>
      <br>

      <div v-if="showBracket">
        <div v-if="numContestants == 4" class="tableContainer">

          <LeftNode
            :indices="[0, 1]"
            :playerSelectionIndex="0"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />

          <PlayoffNode
            :indices="[0, 1]"
            :authorMode="authorMode"
            :teams="teams"
            :playerSelections="playerSelections"
          />

          <RightNode
            :indices="[2, 3]"
            :playerSelectionIndex="1"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />

        </div>

        <div v-else-if="numContestants == 8" class="tableContainer">

          <LeftCluster
            :indices="[0, 1, 2, 3]"
            :playerSelectionIndices="[8, 9]"
            :playerSelectionIndex="12"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />

          <PlayoffCluster
            :indices="[12, 13]"
            :authorMode="authorMode"
            :teams="teams"
            :playerSelections="playerSelections"
          />

          <RightCluster
            :indices="[4, 5, 6, 7]"
            :playerSelectionIndices="[10, 11]"
            :playerSelectionIndex="13"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />

        </div>

        <div v-else-if="numContestants == 16" class="tableContainer">

          <LeftSuperCluster
            :indices="[0, 1, 2, 3, 4, 5, 6, 7]"
            :playerSelectionIndices="[16, 17, 18, 19]"
            :playerSuperIndices="[24, 25]"
            :playerSelectionIndex="28"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />

          <PlayoffSuperCluster
            :indices="[28, 29]"
            :authorMode="authorMode"
            :teams="teams"
            :picksComplete="picksCompleted"
            :playerSelections="playerSelections"
          />

          <RightSuperCluster
            :indices="[8, 9, 10, 11, 12, 13, 14, 15]"
            :playerSelectionIndices="[20, 21, 22, 23]"
            :playerSuperIndices="[26, 27]"
            :playerSelectionIndex="29"
            :authorMode="authorMode"
            :teams="teams"
            :authSelections="authSelections"
            :playerSelections="playerSelections"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LeftNode from '@/components/LeftNode'
import RightNode from '@/components/RightNode'
import LeftCluster from '@/components/LeftCluster'
import RightCluster from '@/components/RightCluster'
import LeftSuperCluster from '@/components/LeftSuperCluster'
import RightSuperCluster from '@/components/RightSuperCluster'
import PlayoffCluster from '@/components/PlayoffCluster'
import PlayoffSuperCluster from '@/components/PlayoffSuperCluster'
import PlayoffNode from '@/components/PlayoffNode'
export default {
  name: 'BracketsGame',
  components: {
    LeftNode,
    RightNode,
    LeftCluster,
    RightCluster,
    LeftSuperCluster,
    RightSuperCluster,
    PlayoffSuperCluster,
    PlayoffNode,
    PlayoffCluster
  },
  data () {
    return {
      showAdmin: true,
      showBracket: true,
      numContestants: 4,
      authorMode: true,
      authSelections: Array(99).fill().map(v => parseInt(1 + Math.random() * 15)),
      playerSelections: Array(99).fill(0),
      lockedPicks: [],
      identifyWinningBracket: false,
      finalResults: [],
      showFinalResults: false,
      cont4: true,
      cont8: false,
      cont16: false,
      teams: [
        {name: null},
        {name: 'Titans'},
        {name: 'Patriots'},
        {name: 'Ravens'},
        {name: 'Steelers'},
        {name: 'Chiefs'},
        {name: 'Chargers'},
        {name: 'Bills'},
        {name: 'Texans'},
        {name: 'Vikings'},
        {name: 'Saints'},
        {name: '49ers'},
        {name: 'Hawks'},
        {name: 'Packers'},
        {name: 'Lions'},
        {name: 'Eagles'}
      ]
    }
  },
  methods: {
    getCurrentPicks () {
      switch (parseInt(this.numContestants)) {
        case 4:
          return this.playerSelections.slice(0, 2)
        case 8:
          return this.playerSelections.slice(8, 14)
        case 16:
          return this.playerSelections.slice(16, 32)
      }
    },
    submitPicks () {
      this.showAdmin = false
      this.lockedPicks = this.getCurrentPicks()
      this.lockedPicks.push(this.playerSelections[98])
      this.authorMode = false
      this.playerSelections = Array(99).fill(0)
      this.identifyWinningBracket = true
    },
    checkPicks () {
      let results = this.getCurrentPicks()
      results.push(this.playerSelections[98])
      this.finalResults = []
      results.forEach((e, idx) => {
        if (this.lockedPicks[idx] === e) {
          this.finalResults.push(this.teams[e].name + ' in Game ' + idx)
        }
      })
      this.showFinalResults = true
      this.showBracket = false
    },
    reset () {
      location.reload()
    }
  },
  watch: {
    numContestants (val) {
      this.playerSelections[98] = 0
      this.cont4 = this.cont8 = this.cont16 = false
      switch (parseInt(val)) {
        case 4: this.cont4 = true; break
        case 8: this.cont8 = true; break
        case 16: this.cont16 = true; break
      }
    }
  },
  computed: {
    picksCompleted () {
      var test = this.numContestants
      switch (this.numContestants) {
        case 4:
          test = this.playerSelections.slice(0, 2).indexOf(0) === -1
          break
        case 8:
          test = this.playerSelections.slice(8, 14).indexOf(0) === -1
          break
        case 16:
          test = this.playerSelections.slice(16, 32).incdexOf(0) === -1
          break
      }
      return test && !!this.playerSelections[98]
    }
  }
}
</script>

<style>
.main{
 height: 100vh;
}
.cont4{
  position: relative;
  top: 30%;
  transform: translateY(-50%);
  transform: scaleX(1.5) scaleY(2.0);
}
.cont8{
  position: relative;
  top: 20%;
  transform: translateY(-50%);
  transform: scaleX(1.2) scaleY(1.7);
}
.cont16{
  position: relative;
  top: 0;
  transform: translateY(-50%);
  transform: scaleX(0.85) scaleY(1.0);
}
</style>
