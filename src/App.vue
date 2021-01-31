<template>
  <div class="admin-panel">
    <header>
      <div class="ring">
        <img :src="FETCHDATA.adminData.avaUrl" />
      </div>
      <div class="title">Ваша панель администратора</div>
    </header>
    <nav>
      <div class="admin-name">
        <div class="wtf">
          {{
            currentSwitchButton === "statistics"
              ? "Статистика администратора"
              : ""
          }}
        </div>
        <div class="first-last-names">
          <div class="firstname">
            {{ FETCHDATA.adminData.firstName }}
          </div>
          <div class="lastname">
            {{ FETCHDATA.adminData.lastName }}
          </div>
          <div class="lvl">{{ FETCHDATA.adminData.lvl }} level</div>
        </div>
      </div>
      <div class="switch-buttons">
        <div
          class="item"
          :class="{ active: item.name === currentSwitchButton }"
          v-for="(item, index) in switchButtons"
          :key="index"
          @click="currentSwitchButton = item.name"
        >
          {{ item.value }}
          <div
            class="new-reps-count"
            v-if="FETCHDATA.adminData.newRepsCount && item.name === 'reps'"
          >
            +{{ FETCHDATA.adminData.newRepsCount }}
          </div>
        </div>
      </div>
      <div class="admin-decency">
        <div class="reprimands">
          <span class="title">Выговоры</span>
          <img
            class="ring"
            :src="
              require(`@/assets/reprimands-ring-${
                n <= FETCHDATA.adminData.reprimands ? 'red' : 'green'
              }.svg`)
            "
            v-for="n in 3"
            :key="n"
          />
        </div>
        <div class="rating">
          <div class="title">Средняя оценка ответа администрации</div>
          <div class="stars">
            <div
              class="star"
              :style="{
                background: `linear-gradient(
              90deg,
              rgba(255, 31, 0, 1) ${ratingGradPercentArray[n - 1]}%,
              rgba(16, 16, 16, 1) ${ratingGradPercentArray[n - 1]}%
            )`,
              }"
              v-for="n in 5"
              :key="n"
            ></div>
          </div>
        </div>
      </div>
      <div class="hidden-title">Prime Role Play Admin Board</div>
    </nav>
    <main :class="{ dark: currentSwitchButton !== 'statistics' }">
      <Statistics v-if="currentSwitchButton === 'statistics'" />
      <Help v-if="currentSwitchButton === 'help'" @modal="modal = $event" />
      <Reps v-if="currentSwitchButton === 'reps'" />
      <MyReps v-if="currentSwitchButton === 'myReps'" />
    </main>
    <div class="blackout" v-if="modal">
      <div class="modal">
        <div class="title">{{ modal.title }}</div>
        <div
          class="custom-input"
          v-if="modal.type === 'l' || modal.type === 'm' || modal.type === 's'"
        >
          <div class="input-title">Укажите ID или ник</div>
          <input type="text" v-model="modal.user" />
        </div>
        <div
          class="custom-input"
          v-if="modal.type === 'l' || modal.type === 'm'"
        >
          <div class="input-title">Укажите причину</div>
          <input type="text" v-model="modal.reason" />
        </div>
        <div class="custom-input" v-if="modal.type === 'l'">
          <div class="input-title">Укажите длительность</div>
          <input type="text" v-model="modal.duration" />
        </div>
        <div class="buttons">
          <div class="item">Выполнить</div>
          <div class="item" @click="modal = false">Отменить</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Statistics from "@/components/statistics.vue";
import Reps from "@/components/reps.vue";
import Help from "@/components/help.vue";
import MyReps from "@/components/myReps.vue";

export default {
  name: "App",
  data() {
    return {
      FETCHDATA: {
        adminData: {
          firstName: "Romario",
          lastName: "Richardson",
          avaUrl: "/header-ava.png",
          lvl: 8,
          newRepsCount: 1234,
          reprimands: 2,
          rating: 3.3,
        },
      },
      modal: false,
      currentSwitchButton: "statistics",
      switchButtons: [
        {
          name: "statistics",
          value: "Главная страница",
        },
        {
          name: "reps",
          value: "Репорты",
        },
        {
          name: "help",
          value: "Помощь",
        },
        {
          name: "myReps",
          value: "Мои репорты",
        },
        {
          name: "exit",
          value: "Выход",
        },
      ],
    };
  },
  computed: {
    ratingGradPercentArray() {
      const rating = this.FETCHDATA.adminData.rating;
      let arr = [0, 0, 0, 0, 0];
      for (let i = 1; i <= rating; i++) {
        if (rating - i >= 1) {
          arr[i - 1] = 100;
          continue;
        }
        arr[i - 1] = 100;
        arr[i] = (rating - i) * 100;
      }
      return arr;
    },
  },
  components: {
    Statistics,
    Reps,
    Help,
    MyReps,
  },
};
</script>

<style lang="scss">
@font-face {
  font-family: Bebas Neue;
  src: url("~@/assets/Bebas Neue Bold.ttf");
  font-weight: 600;
}

@font-face {
  font-family: Bebas Neue;
  src: url("~@/assets/Bebas Neue Book.ttf");
  font-weight: 200;
}

@font-face {
  font-family: Bebas Neue;
  src: url("~@/assets/Bebas Neue Regular.ttf");
  font-weight: 400;
}

html {
  font-family: Bebas Neue;
  font-size: 0.9375vw;
  line-height: 1;
  color: #fff;
}

body {
  margin: 0;
  background: url("https://images.hdqwalls.com/download/gta-v-ferrari-8k-4x-1920x1080.jpg")
    no-repeat;
}

.admin-panel {
  display: flex;
  height: 100vh;
  width: 100vw;
  position: relative;

  header {
    box-sizing: border-box;
    padding: 2.60416vw 0 5.2083vw 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 6.71875vw;
    height: inherit;
    background-color: rgba(18, 18, 26, 0.95);

    .ring {
      padding: 0.3125vw;
      border-radius: 50%;
      background: linear-gradient(
        131.32deg,
        #c90000 17.48%,
        rgba(255, 0, 0, 0) 92.13%
      );
      filter: drop-shadow(0px 0px 1vw rgba(255, 0, 0, 0.85));

      img {
        display: block;
        width: 3.28125vw;
        height: 3.28125vw;
      }
    }

    .title {
      writing-mode: vertical-lr;
      transform: rotate(180deg);
      font-weight: bold;
      font-size: 4rem;
      white-space: nowrap;
      opacity: 0.25;
    }
  }

  nav {
    box-sizing: border-box;
    padding: 2.60416vw 0 5.2083vw 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 26.97916vw;
    height: inherit;
    background-color: rgba(18, 18, 26, 0.85);
    position: relative;

    .wtf {
      height: 1rem;
    }

    .first-last-names {
      margin-top: 1.8229166vw;
      font-weight: bold;
      font-size: 4rem;
      line-height: 1;
      position: relative;

      .lvl {
        writing-mode: vertical-lr;
        transform: rotate(180deg);
        font-size: 2.1rem;
        white-space: nowrap;
        position: absolute;
        bottom: 0.833vw;
        right: 100%;
      }
    }

    .switch-buttons {
      .item {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 0.3645833vw;
        width: 14.375vw;
        height: 2.96875vw;
        font-size: 1.333rem;
        color: rgba(255, 255, 255, 0.65);
        border-radius: 0.20833vw;
        position: relative;

        &.active {
          color: rgba(21, 21, 21, 0.9);
          background-color: #fff;
          box-shadow: 0px 0px 0.3125vw rgba(255, 255, 255, 0.75);
        }

        .new-reps-count {
          box-sizing: border-box;
          padding: 0 0.2083333333vw;
          line-height: 1.09375vw;
          background-color: #8fff00;
          border-radius: 0.2083333333vw;
          color: #000;
          font-size: 1rem;
          box-shadow: 0px 0px 0.3125vw rgba(143, 255, 0, 0.75);
          position: absolute;
          top: 50%;
          left: 9.6354166667vw;
          transform: translateY(-50%);
        }
      }
    }

    .admin-decency {
      width: 14.375vw;

      .reprimands {
        display: flex;
        align-items: center;
        margin-bottom: 2.0833vw;

        .title {
          margin-right: 0.3645833vw;
        }

        .ring {
          width: 1.40625vw;
        }
      }

      .rating {
        width: 14.375vw;

        .title {
          margin-bottom: 1.04166vw;
        }

        .stars {
          display: flex;
          justify-content: space-between;
          width: inherit;

          .star {
            display: block;
            height: 2.395833vw;
            width: 2.395833vw;
            mask-image: url("~@/assets/rating-star.svg");
            mask-repeat: no-repeat;
            mask-position: center;
            mask-size: contain;
          }
        }
      }
    }

    .hidden-title {
      color: rgba(255, 255, 255, 0.1);
      position: absolute;
      left: 50%;
      bottom: 0.625vw;
      transform: translate(-50%);
    }
  }

  main {
    box-sizing: border-box;
    padding-top: 2.60416vw;
    display: flex;
    justify-content: center;
    flex-grow: 1;

    &.dark {
      background-color: rgba(18, 18, 26, 0.75);
    }
  }

  .blackout {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;

    .modal {
      box-sizing: border-box;
      padding: 1.8229166667vw;
      width: 22.8125vw;
      background: linear-gradient(
        226deg,
        rgba(18, 18, 25, 0.95) 1.97%,
        rgba(25, 25, 45, 0.95) 99.42%
      );

      .title {
        font-weight: bold;
        font-size: 1.6666666667rem;
        margin-bottom: 3.4375vw;
        position: relative;

        &::after {
          content: "";
          background: linear-gradient(90.63deg, #ff1f00 0%, #6d0d00 99.57%);
          border-radius: 0.1041666667vw;
          width: 1.8229166667vw;
          height: 0.2604166667vw;
          position: absolute;
          top: calc(100% + 0.4166666667vw);
          left: 0;
        }
      }

      .custom-input {
        margin-bottom: 1.5104166667vw;

        .input-title {
          margin-bottom: 0.2083333333vw;
        }

        input {
          box-sizing: border-box;
          padding: 0.8333333333vw;
          border: none;
          border-radius: 0.2083333333vw;
          background: rgba(0, 0, 0, 0.4);
          font-family: Bebas Neue;
          font-size: 1.0416666667vw;
          color: #fff;
          text-align: center;
          outline: none;
          width: 100%;

          &::placeholder {
            color: rgba(255, 255, 255, 0.09);
          }
        }
      }

      .buttons {
        display: flex;
        justify-content: space-between;
        margin-top: 2.8125vw;

        .item {
          box-sizing: border-box;
          width: 9.1145833333vw;
          line-height: 1.9791666667vw;
          text-align: center;
          border: 0.0520833333vw solid #fff;
          border-radius: 0.2083333333vw;

          &:hover {
            box-shadow: 0px 0px 6px rgba(255, 255, 255, 0.75);
            background: #fff;
            color: rgba(21, 21, 21, 0.9);
          }
        }
      }
    }
  }
}
</style>
