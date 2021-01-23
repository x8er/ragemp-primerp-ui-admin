<template>
  <div class="admin-panel">
    <header>
      <div class="ring">
        <img src="/header-ava.png" />
      </div>
      <div class="title">Ваша панель администратора</div>
    </header>
    <nav>
      <div class="admin-name">
        <div class="wtf">Статистика администратора</div>
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
              rgba(255, 31, 0, 1) ${ratingGradPercent[n - 1]}%,
              rgba(16, 16, 16, 1) ${ratingGradPercent[n - 1]}%
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
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      FETCHDATA: {
        adminData: {
          firstName: "Romario",
          lastName: "Richardson",
          lvl: 8,
          reprimands: 2,
          rating: 3.3,
        },
      },
      currentSwitchButton: "main",
      switchButtons: [
        {
          name: "main",
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
    ratingGradPercent() {
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
};
</script>

<style lang="scss">
@font-face {
  font-family: Bebas Neue;
  src: url("~@/assets/Bebas Neue Bold.ttf");
  font-weight: bold;
}

@font-face {
  font-family: Bebas Neue;
  src: url("~@/assets/Bebas Neue Regular.ttf");
}

html {
  font-family: Bebas Neue;
  font-size: 0.9375vw;
  line-height: 1;
  color: #fff;
}

body {
  margin: 0;
}

.admin-panel {
  display: flex;
  height: 100vh;
  width: 100vw;

  header {
    box-sizing: border-box;
    padding: 2.60416vw 0 5.2083vw 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 6.71875vw;
    height: inherit;
    background: linear-gradient(
      180deg,
      rgba(18, 18, 25, 0.85) 0%,
      rgba(18, 18, 26, 0.85) 100%
    );

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
      opacity: 0.15;
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
    background: linear-gradient(
      180deg,
      rgba(18, 18, 25, 0.65) 0%,
      rgba(18, 18, 26, 0.65) 100%
    );
    position: relative;

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
        color: rgba(255, 255, 255, 0.45);
        border-radius: 0.20833vw;

        &.active {
          color: rgba(21, 21, 21, 0.9);
          background-color: #fff;
          box-shadow: 0px 0px 0.3125vw rgba(255, 255, 255, 0.75);
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
}
</style>
