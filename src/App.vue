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
    <main>
      <div class="statistics">
        <div class="lil-stats">
          <div class="stats">
            <div class="title">Статистика онлайна администратора</div>
            <div class="main">
              <div class="name">
                <div class="dot"></div>
                <span>Часов</span>
              </div>
              <div class="value">
                {{ FETCHDATA.adminData.online[currentOnlineSort] }}
              </div>
              <div class="sort">
                <div
                  class="item"
                  :class="{ active: currentOnlineSort === 0 }"
                  @click="currentOnlineSort = 0"
                >
                  За день
                </div>
                <div
                  class="item"
                  :class="{ active: currentOnlineSort === 1 }"
                  @click="currentOnlineSort = 1"
                >
                  За неделю
                </div>
                <div
                  class="item"
                  :class="{ active: currentOnlineSort === 2 }"
                  @click="currentOnlineSort = 2"
                >
                  За месяц
                </div>
              </div>
            </div>
          </div>
          <div class="stats">
            <div class="title">Статистика ответов администратора</div>
            <div class="main">
              <div class="name">
                <div class="dot"></div>
                <span>Репортов</span>
              </div>
              <div class="value">
                {{ FETCHDATA.adminData.answer[currentAnswerSort] }}
              </div>
              <div class="sort">
                <div
                  class="item"
                  :class="{ active: currentAnswerSort === 0 }"
                  @click="currentAnswerSort = 0"
                >
                  За день
                </div>
                <div
                  class="item"
                  :class="{ active: currentAnswerSort === 1 }"
                  @click="currentAnswerSort = 1"
                >
                  За неделю
                </div>
                <div
                  class="item"
                  :class="{ active: currentAnswerSort === 2 }"
                  @click="currentAnswerSort = 2"
                >
                  За месяц
                </div>
              </div>
            </div>
          </div>
          <div class="stats">
            <div class="title">Статистика времени ответа</div>
            <div class="main">
              <div class="name">
                <div class="dot"></div>
                <span>В среднем</span>
              </div>
              <div class="value">
                {{ FETCHDATA.adminData.timing[currentTimingSort] }} СЕК
              </div>
              <div class="sort">
                <div
                  class="item"
                  :class="{ active: currentTimingSort === 0 }"
                  @click="currentTimingSort = 0"
                >
                  За день
                </div>
                <div
                  class="item"
                  :class="{ active: currentTimingSort === 1 }"
                  @click="currentTimingSort = 1"
                >
                  За неделю
                </div>
                <div
                  class="item"
                  :class="{ active: currentTimingSort === 2 }"
                  @click="currentTimingSort = 2"
                >
                  За месяц
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="detailed-online-statistics">
          <div class="title">Детальная статистика онлайна администратора</div>
          <div class="main">
            <div class="scale">
              <div class="item">12 ч</div>
              <div class="item">11 ч</div>
              <div class="item">10 ч</div>
              <div class="item">9 ч</div>
              <div class="item">8 ч</div>
              <div class="item">7 ч</div>
              <div class="item">6 ч</div>
              <div class="item">5 ч</div>
              <div class="item">4 ч</div>
              <div class="item">3 ч</div>
              <div class="item">2 ч</div>
              <div class="item">1 ч</div>
            </div>
            <div class="bar-chart">
              <div
                class="item"
                :style="{ height: secondToPercentArray[index] + '%' }"
                v-for="(item, index) in FETCHDATA.adminData.week"
                :key="index"
              >
                <div class="day-name">{{ item.dayName }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
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
          online: [8, 54, 454],
          answer: [1356, 10778, 32588],
          timing: [30, 42, 34],
          week: [
            {
              dayName: "пн",
              value: 21600,
            },
            {
              dayName: "вт",
              value: 7200,
            },
            {
              dayName: "ср",
              value: 10800,
            },
            {
              dayName: "чт",
              value: 25200,
            },
            {
              dayName: "пт",
              value: 18000,
            },
            {
              dayName: "сб",
              value: 32400,
            },
            {
              dayName: "вс",
              value: 28800,
            },
          ],
        },
      },
      currentOnlineSort: 0,
      currentAnswerSort: 0,
      currentTimingSort: 0,
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
    secondToPercentArray() {
      return this.FETCHDATA.adminData.week.map((el) => {
        return Math.ceil((el.value * 100) / 43200);
      });
    },
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

  main {
    box-sizing: border-box;
    padding-top: 2.60416vw;
    display: flex;
    justify-content: center;
    flex-grow: 1;

    .statistics {
      width: 49.53125vw;

      .lil-stats {
        display: flex;
        justify-content: space-between;
        width: inherit;
        margin-bottom: 1.40625vw;

        .stats {
          .title {
            margin-bottom: 0.520833vw;
          }

          .main {
            box-sizing: border-box;
            padding: 0.8854166vw;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            width: 14.9479166vw;
            height: 7.96875vw;
            background: linear-gradient(
              180deg,
              rgba(18, 18, 25, 0.85) 0%,
              rgba(18, 18, 26, 0.85) 100%
            );
            border-radius: 0.20833vw;

            .name {
              display: flex;
              align-items: center;

              .dot {
                width: 0.3125vw;
                height: 0.3125vw;
                background: #00ff85;
                box-shadow: 0px 0px 0.3125vw rgba(0, 255, 133, 0.5);
                border-radius: 50%;
                margin-right: 0.729166vw;
              }

              span {
                font-weight: lighter;
                color: rgba(255, 255, 255, 0.25);
              }
            }

            .value {
              font-weight: bold;
              font-size: 3.55rem;
              text-align: center;
              text-shadow: 0px 0px 0.22rem rgba(255, 255, 255, 0.25);
            }

            .sort {
              display: flex;
              justify-content: space-between;

              .item {
                color: rgba(255, 255, 255, 0.15);

                &.active {
                  color: #fff;
                  position: relative;

                  &::after {
                    content: "";
                    width: 100%;
                    height: 0.11rem;
                    background-color: #d9203c;
                    position: absolute;
                    top: 120%;
                    left: 0;
                  }
                }
              }
            }
          }
        }
      }

      .detailed-online-statistics {
        .title {
          margin-bottom: 0.520833vw;
        }

        .main {
          box-sizing: border-box;
          padding: 0.8854166vw 0.8854166vw 2.0833333333vw 0.8854166vw;
          display: flex;
          background: linear-gradient(
            180deg,
            rgba(18, 18, 25, 0.85) 0%,
            rgba(18, 18, 26, 0.85) 100%
          );
          border-radius: 0.20833vw;

          .scale {
            .item {
              color: rgba(255, 255, 255, 0.16);
              margin-bottom: 0.6770833333vw;
            }
          }

          .bar-chart {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            flex-grow: 1;
            margin: 0 2.0833333333vw;

            .item {
              width: 3.3854166667vw;
              background: linear-gradient(180deg, #c41e37 0%, #ff0027 100%);
              box-shadow: 0px 0px 0.6770833333vw -0.15625vw #ff1f00;
              border-radius: 0.20833vw;
              position: relative;

              .day-name {
                color: rgba(255, 255, 255, 0.16);
                position: absolute;
                bottom: -1.3541666667vw;
                left: 50%;
                transform: translateX(-50%);
              }
            }
          }
        }
      }
    }
  }
}
</style>
