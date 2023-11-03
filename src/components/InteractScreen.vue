<script>
import CardFlip from './Card.vue'
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  components: {
    CardFlip
  },
  data() {
    return {
      rules: []
    }
  },
  methods: {
    checkRule(card) {
      console.log(this.rules)
      if (this.rules.length === 2) return false
      this.rules.push(card)
      if (this.rules.length === 2 && this.rules[0].value === this.rules[1].value) {
        console.log('right')
        this.rules = []
      } else if (this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
        console.log('wrong')
        this.$refs[`card-${this.rules[0].index}`].onFlipBackCard()
        this.$refs[`card-${this.rules[1].index}`].onFlipBackCard()
        this.rules = []
      }
      return false
    }
  }
}
</script>

<template>
  <div class="screen">
    <h1>Interact screen</h1>
    <CardFlip
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceUrl="`src/assets/images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="checkRule($event)"
    />
  </div>
</template>
