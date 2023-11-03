<!-- eslint-disable vue/multi-word-component-names -->
<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object]
    },
    imgBackFaceUrl: {
      type: String,
      required: true
    },
    cardsContext: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  data() {
    return {
      isDisabled: false,
      isFlipped: false
    }
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false
      this.isFlipped = !this.isFlipped
      if (this.isFlipped) this.$emit('onFlip', this.card)
    },

    onFlipBackCard() {
      this.isFlipped = false
    },

    onEnabledDisableMode() {
      this.isDisabled = true
    }
  }
}
</script>

<template>
  <div class="card">
    <div class="card_inner" :class="{ 'is-flipped': isFlipped }" @click="onToggleFlipCard">
      <div class="card_face card_face-front">
        <div class="card_content"></div>
      </div>
      <div class="card_face card_face-back">
        <div class="card_content" :style="{ backgroundImage: `url('${imgBackFaceUrl}')` }"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 90px;
  height: 120px;
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card_inner.is-flipped {
  transform: rotateY(-180deg);
}

.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card_face-front .card_content {
  background: url('../assets/images/icon_back.png') no-repeat center center;
  background-size: 50px 50px;
  height: 100%;
  width: 100%;
}

.card_face-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card_face-back .card_content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
