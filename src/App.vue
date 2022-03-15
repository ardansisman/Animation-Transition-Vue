<template>
  <transition-group name="slideContainer" mode="out-in">
    <component
      key="mainComponent"
      @activeComponentEvent="activeComponent = $event"
      :is="activeComponent"
    >
    </component>
    <canvas v-show="activeComponent == 'app-celebrate'" key="canvas" id="canvas"></canvas>
  </transition-group>
</template>
<script>
import GameCards from "./components/GameCards.vue";
import Failure from "./components/Failure.vue";
import Celebrate from "./components/Celebrate.vue";
export default {
  data() {
    return { activeComponent: "app-Game-Cards" };
  },
  components: {
    appGameCards: GameCards,
    appFailure: Failure,
    appCelebrate: Celebrate,
  },
};
</script>
<style>
.body {
  font-family: sans-serif;
}

.slideContainer-enter {
}
.slideContainer-enter-active {
  animation: slide-in 0.3s ease-out forwards;
}
.slideContainer-leave {
}
.slideContainer-leave-enter {
  animation: slide-out 0.3s ease-out forwards;
}

@keyframes slide-in {
  from {
    transform: translateX(-1000px);
    opacity: 0;
  }
  to {
    transform: translateX(0px);
    opacity: 1;
  }
}

@keyframes slide-out {
  from {
    transform: translateX(0px);
    opacity: 1;
  }
  to {
    transform: translateX(1000px);
    opacity: 0;
  }
}
</style>
