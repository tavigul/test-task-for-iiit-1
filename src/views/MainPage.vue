<template>
  <div class="cards-wrapper">
    <div class="cards">
      <CardComponent
        v-for="(card, index) in cards"
        :key="index"
        :is-flipped="card.flipped"
        :is-lifted="card.lifted"
        :number="card.number"
        :sign="card.sign"
        @click="toggleCard(index)"
      />
    </div>
    <button class="button" @click="flipAndLiftCard">Flip and Lift Card</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import CardComponent from "../components/CardComponent.vue";

interface CardState {
  flipped: boolean;
  lifted: boolean;
  number: string;
  sign: string;
}

export default defineComponent({
  name: "MainPage",
  components: {
    CardComponent,
  },
  setup() {
    const cards = ref<CardState[]>([
      { flipped: false, lifted: false, number: "A", sign: "♠" },
      { flipped: false, lifted: false, number: "2", sign: "♣" },
      { flipped: false, lifted: false, number: "3", sign: "♦" },
    ]);

    const toggleCard = (index: number) => {
      const card = cards.value[index];
      card.flipped = !card.flipped;
    };

    const flipAndLiftCard = () => {
      const middleCardIndex = Math.floor(cards.value.length / 2);
      const middleCard = cards.value[middleCardIndex];

      // If the card is already flipped and lifted, revert to initial state
      if (middleCard.flipped && middleCard.lifted) {
        middleCard.flipped = false;
        middleCard.lifted = false;
      } else {
        // Otherwise, flip and lift the card
        middleCard.flipped = true;
        middleCard.lifted = true;
      }
    };

    return {
      cards,
      flipAndLiftCard,
      toggleCard,
    };
  },
});
</script>

<style>
.cards-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  justify-content: center;
}

.cards {
  display: flex;
  justify-content: space-between;
  gap: 30px;
}

.button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 50px;
}

@media (max-width: 768px) {
  .cards {
    width: 100%;
    align-items: flex-start;
    gap: 10px;
    flex-wrap: wrap;
    justify-content: center;
    flex-direction: row;
  }

  .cards > *:first-child {
    order: 2;
    margin-bottom: -100px;
  }

  .button {
    margin-top: 120px;
  }
}
</style>
