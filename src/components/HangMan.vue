<template>
  <div id="app">
    <div id="conditionalrendering">
      <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="350px" height="275px" viewBox="0 0 350 300" preserveAspectRatio="xMidYMid meet">
        <line v-if="strikes > 0" x1="80" y1="257" x2="260" y2="257" style="stroke:black;" />
        <line v-if="strikes > 1" x1="100" y1="257" x2="100" y2="40" style="stroke:black;" />
        <line v-if="strikes > 2" x1="100" y1="40" x2="230" y2="40" style="stroke:black;" />
        <line v-if="strikes > 3" x1="100" y1="80" x2="130" y2="40" style="stroke:black;" />
        <line v-if="strikes > 4" x1="230" y1="40" x2="230" y2="80" style="stroke:black;" />
        <circle v-if="strikes > 5" cx="230" cy="90" style="fill:khaki;stroke:black;" r="20" />
        <line v-if="strikes > 6" x1="230" y1="110" x2="230" y2="170" style="stroke:black;" />
        <line v-if="strikes > 7" x1="230" y1="140" x2="250" y2="120" style="stroke:black;" />
        <line v-if="strikes > 8" x1="230" y1="140" x2="210" y2="120" style="stroke:black;" />
        <line v-if="strikes > 9" x1="230" y1="170" x2="250" y2="200" style="stroke:black;" />
        <line v-if="strikes > 10" x1="230" y1="170" x2="210" y2="200" style="stroke:black;" />
      </svg>
    </div>
    <div id="eventlistener">
        <!-- the @click listener will call the tryLetter method after the click event
        on one of the letters -->
        <div>
          <div v-for="letter in displayLetters" class="letter">
            {{ letter }}
          </div>
        </div>
        <div>
          <div @click="tryLetter(letter)" v-for="letter in possibleLetters" class="possibleLetter">
            {{ letter }}
          </div>
        </div>
        <div>
        {{console}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HangMan',
  props: {
    msg: String,
  },
  data() {
    return {
      displayLetters: ['','','',''],
      wordLetters: ['C','O','O','L'],
      possibleLetters: ['A', 'B', 'C', 'L', 'O'],
      console: 'Click a letter above to see the result',
      strikes: 0,
    }
  },
  methods: {
    tryLetter(letter) {
      for (let i = 0; i < this.displayLetters.length; i++) {
        if (letter === this.wordLetters[i]) {
          this.displayLetters.splice(i, 1, letter)
        }
      }
      this.console = 'I tried letter ' + letter
    },
    addStrike() {
      this.strikes++
    }  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
