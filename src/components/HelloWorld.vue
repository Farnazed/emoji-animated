<template>
  <div class="emojiwrapper">
    <p class="drop">
      <span class="pumpkin">{{ randomEmoji }}</span>
    </p>
  </div>
</template>
<script>
export default {
  computed: {
    randomEmoji() {
      return String.fromCodePoint(
        '0x' +
          ['1F47B', '1F383', '1f9df', '1F479'][Math.floor(Math.random() * 4)]
      );
    },
  },
};
</script>
<style scoped>
.emojiwrapper {
  display: flex;
}

.pumpkin {
  font-size: 4rem;
}

.drop:hover {
  animation: wiggle ease-in 0.5s;
  animation-fill-mode: none;
}

.drop {
  animation: drop ease-in 0.5s;
  animation-fill-mode: both;
}
@keyframes drop {
  0% {
    transform: translatey(-100px);
  }
  60% {
    transform: translatey(0px) scale(1.2, 1);
  }
  70% {
    transform: translatey(-10px) scale(1, 1);
  }
  100% {
    transform: translatey(0px) rotatez(0deg);
  }
}

@keyframes wiggle {
  0% {
    transform: rotatez(0deg);
  }
  20% {
    transform: rotatez(30deg);
  }
  40% {
    transform: rotatez(-30deg);
  }
  60% {
    transform: rotatez(20deg);
  }
  80% {
    transform: rotatez(-20deg);
  }
  100% {
    transform: rotatez(0deg);
  }
}
</style>
