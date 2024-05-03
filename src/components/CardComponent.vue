<template>
  <div
    class="card"
    :class="{ flipped: isFlipped, lifted: isLifted }"
    @click="handleClick"
  >
    <div class="card-front"></div>
    <div class="card-back"></div>
    <div class="card-content">
      <div class="number" v-if="isFlipped">{{ number }}</div>
      <div class="sign" v-if="isFlipped">{{ sign }}</div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CardComponent",
  props: {
    isFlipped: {
      type: Boolean,
      default: false,
    },
    isLifted: {
      type: Boolean,
      default: false,
    },
    number: {
      type: String,
      default: "",
    },
    sign: {
      type: String,
      default: "",
    },
  },
  methods: {
    handleClick() {
      this.$emit("click");
    },
  },
});
</script>

<style scoped>
.card {
  width: 180px;
  height: 270px;
  border-radius: 20px;
  position: relative;
  perspective: 1000px;
  background-color: #142c50;
  border: 3px solid #575864;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1), background-color 0.5s;
}
.card.flipped {
  transform: rotateY(180deg);
  background-color: white;
}

.card.lifted {
  transform: translateY(-150px);
}

.card.lifted.flipped {
  transform: translateY(-150px) rotateY(360deg);
}

.card-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  color: black;
  font-size: 35px;
  padding: 16px;
  font-weight: bold;
  backface-visibility: hidden;
}

.card-content.flipped {
  display: none;
}

.card-content.flipped .number,
.card-content.flipped .sign {
  display: block;
}

.card-back {
  display: none;
}

.card-front.flipped {
  display: none;
}

@media (max-width: 768px) {
  .card {
    width: 120px;
    height: 180px;
  }
  .card-content {
    font-size: 22px;
  }
}
</style>
