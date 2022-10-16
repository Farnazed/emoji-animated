<template>
  <div class="emojiwrapper">
    <p class="drop">
      <span class="pumpkin">{{ randomEmoji }}</span>
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      holidays: {
        halloween: {
          from: '10-15',
          to: '10-31',
          emojis: ['1F47B', '1F383', '1f9df', '1F479'],
        },
        christmas: {
          from: '12-20',
          to: '12-25',
          emojis: ['1F384', '1F381', '2603', '1F385'],
        },
        // newYear: {
        //   from: '12-26',
        //   to: '01-01',
        //   emojis: ['1F47B', '1F383', '1f9df', '1F479'],
        // },
      },
    };
  },
  computed: {
    randomEmoji() {
      let holidayPack = null;
      let currentDate = new Date();
      let currentDay = currentDate.getDate();
      let currentMonth = currentDate.getMonth() + 1;
      for (const occasion in this.holidays) {
        let from = {
          month: parseInt(this.holidays[occasion].from.split('-')[0]),
          day: parseInt(this.holidays[occasion].from.split('-')[1]),
        };
        let to = {
          month: parseInt(this.holidays[occasion].to.split('-')[0]),
          day: parseInt(this.holidays[occasion].to.split('-')[1]),
        };

        if (
          currentMonth <= to.month &&
          currentMonth >= from.month &&
          currentDay <= to.day &&
          currentDay >= from.day
        ) {
          holidayPack = this.holidays[occasion];
        }
      }
      return holidayPack
        ? String.fromCodePoint(
            '0x' + holidayPack.emojis[Math.floor(Math.random() * 4)]
          )
        : '';
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
