<template>
  <div class="game-area">
    <h1 class="title">Poğaça <span> Nerede </span> <strong>?</strong></h1>
    <h4 class="description">
      Açık kartlardan birini seçtikten sonra, kapalı olan karta tıklayınız.
    </h4>
    <div class="container">
      <transition-group name="rotate-all" class="card-container" appear>
        <app-card
          :class="{ shadow: selectedCard == card.id }"
          @click.native="selectedCard = card.id"
          :key="card.id"
          v-for="card in cards"
          :card="card"
        >
        </app-card>
      </transition-group>
    </div>
    <div class="container">
      <transition name="rotate" mode="out-in">
        <component
          @click.native="showCard(answer)"
          :is="activeCard"
          :card="answer"
        ></component>
      </transition>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
import DefaultCard from "./DefaultCard.vue";
import Celebrate from "./Celebrate.vue";

export default {
  components: {
    appCard: Card,
    appDefaultCard: DefaultCard,
    appCelebrate: Celebrate,
  },
  data() {
    return {
      selectedCard: null,
      answer: {},
      activeCard: "app-default-card",
      cards: [
        { id: 1, component: "app-card", image: "/src/assets/card-1.jpg" },
        { id: 2, component: "app-card", image: "/src/assets/card-2.jpg" },
        { id: 3, component: "app-card", image: "/src/assets/card-3.jpg" },
        { id: 4, component: "app-card", image: "/src/assets/card-4.jpg" },
        { id: 5, component: "app-card", image: "/src/assets/card-5.jpg" },
      ],
    };
  },
  created() {
    let answer = Math.ceil(Math.random() * this.cards.length);
    this.answer = this.cards[answer - 1];
  },
  methods: {
    showCard(answer) {
      if (this.selectedCard == null) {
        alert("Lütfen açık kartlardan seçim yapınız.");
      } else {
        this.activeCard = answer.component;
        setTimeout(() => {
          if (answer.id == this.selectedCard) {
            this.$emit("activeComponentEvent", "app-celebrate");
          } else {
            this.$emit("activeComponentEvent", "app-failure");
          }
        }, 2000);
      }
    },
  },
};
</script>

<style scoped>
.title {
  text-align: center;

  color: rosybrown;
}
.title span {
  color: mediumpurple;
}
.title strong {
  color: darkred;
}
.description {
  color: grey;
  text-align: center;
}
.container,
.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50px;
}
.shadow {
  box-shadow: 0px 5px 48px #30969f !important;
  transition: box-shadow 0.5s;
}

/**Açık kartların animasyonları için gerekli olan transition class tanımlamarı */
.rotate-all-enter {
}
.rotate-all-enter-active {
  animation: rotate-all ease-in-out 0.5s forwards;
}
.rotate-all-leave {
}
.rotate-all-leave-active {
}

@keyframes rotate-all {
  from {
    transform: rotateY(0);
  }
  to {
    transform: rotateY(720deg);
  }
}

/**Açık kartın animasyonları için gerekli olan transition class tanımlamarı */
.rotate-enter {
}
.rotate-enter-active {
  animation: rotate-in ease-in-out 1s forwards;
}
.rotate-leave {
}
.rotate-leave-active {
  animation: rotate-out ease-in-out 1s forwards;
}

@keyframes rotate-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}

@keyframes rotate-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}
</style>

