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
      <div class="statistics" v-if="currentSwitchButton === 'statistics'">
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
        <div class="news">
          <div class="title">Новости</div>
          <div class="main">
            <div class="ava">
              <img src="/news-ava.png" />
            </div>
            <div class="container">
              <div class="info">
                <div class="user">
                  <div class="rang-title">{{ FETCHDATA.news.rangTitle }}</div>
                  <div class="fullname">
                    {{
                      FETCHDATA.news.firstName + " " + FETCHDATA.news.lastName
                    }}
                  </div>
                </div>
                <div class="timestamp">{{ millisecondsToDateString }}</div>
              </div>
              <div class="message">{{ FETCHDATA.news.message }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="help" v-if="currentSwitchButton === 'help'">
        <div class="title">Команды для взаимодействия с сервером</div>
        <div class="list">
          <div
            class="item"
            v-for="(item, index) in FETCHDATA.adminData.commands"
            :key="index"
            @click="modal = { ...item }"
          >
            {{ item.title }}
          </div>
        </div>
      </div>
      <div class="reps" v-if="currentSwitchButton === 'reps'">
        <div class="title">Взаимодействие с репортами</div>
        <div class="list">
          <div
            class="item"
            v-for="(item, index) in FETCHDATA.reps"
            :key="index"
          >
            <div class="report" @click="openRepsChat(index)">
              <div class="user-data">
                <img :src="require('@/assets/reps-ava.svg')" class="logo" />
                <div class="data">
                  <div class="timing">
                    {{ millisecondsToTimeStringArray[index] }}
                  </div>
                  <div class="name">
                    {{ item.firstName + " " + item.lastName }}
                  </div>
                  <div class="ids">[{{ item.id }}], #{{ item.accId }}</div>
                </div>
              </div>
              <div class="report-info">
                <div class="report-afk">
                  Репорт без ответа <span>{{ afkTime(item.time) }}</span> сек.
                </div>
                <div class="report-text">{{ item.text }}</div>
              </div>
              <div class="report-status">
                <div class="check-row">
                  <div class="title">Проверяет:</div>
                  <div
                    class="check"
                    :class="{ 'not-empty': item.checkingAdmin }"
                  >
                    {{
                      !item.checkingAdmin
                        ? "Свободный тикет"
                        : item.checkingAdmin
                    }}
                  </div>
                </div>
                <div class="type-row">
                  <div class="title">Тип обращения:</div>
                  <div class="type" :class="{ question: item.type }">
                    {{ !item.type ? "Жалоба" : "Вопрос" }}
                  </div>
                </div>
                <div
                  class="btn"
                  :class="{ free: !item.closed && !item.checkingAdmin }"
                >
                  {{ !item.checkingAdmin && !item.closed ? "Забрать" : "" }}
                  {{ item.checkingAdmin && !item.closed ? "Недоступно" : "" }}
                  {{ item.checkingAdmin && item.closed ? "Закрыто" : "" }}
                </div>
              </div>
              <div
                class="user-privilege"
                :class="{ [item.privilege]: item.privilege }"
                v-if="item.privilege"
              >
                {{
                  item.privilege === "vip-plus"
                    ? item.privilege.replace("-plus", "+")
                    : item.privilege
                }}
              </div>
              <img
                :src="require('@/assets/reps-arrow.svg')"
                class="arrow-logo"
                :class="{ active: repsChat === index }"
              />
            </div>
            <div class="chat" :class="{ active: repsChat === index }">
              <div class="history">
                <div
                  class="message"
                  :class="{ admin: item.admin }"
                  v-for="(item, index) in item.history"
                  :key="index"
                >
                  <div class="ava">
                    <img :src="item.avaUrl" />
                    <div class="online"></div>
                  </div>
                  <div class="data">
                    <div class="name">
                      {{ item.firstName + " " + item.lastName }}
                    </div>
                    <div class="text">
                      {{ item.text }}
                    </div>
                    <div class="timing">
                      {{ millisecondsToTimeString(item.time) }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="my-reps" v-if="currentSwitchButton === 'myReps'">
        <div class="title">Взаимодействие с репортами</div>
        <div class="list">
          <div
            class="item"
            v-for="(item, index) in FETCHDATA.myReps"
            :key="index"
          >
            <div class="report" @click="openMyRepsChat(index)">
              <div class="user-data">
                <img :src="require('@/assets/reps-ava.svg')" class="logo" />
                <div class="data">
                  <div class="timing">
                    {{ millisecondsToTimeStringArray[index] }}
                  </div>
                  <div class="name">
                    {{ item.firstName + " " + item.lastName }}
                  </div>
                  <div class="ids">[{{ item.id }}], #{{ item.accId }}</div>
                </div>
              </div>
              <div class="report-info">
                <div class="report-text">{{ item.text }}</div>
              </div>
              <div class="report-status">
                <div class="check-row">
                  <div class="title">Проверяет:</div>
                  <div
                    class="check"
                    :class="{ 'not-empty': item.checkingAdmin }"
                  >
                    {{
                      !item.checkingAdmin
                        ? "Свободный тикет"
                        : item.checkingAdmin
                    }}
                  </div>
                </div>
                <div class="type-row">
                  <div class="title">Тип обращения:</div>
                  <div class="type" :class="{ question: item.type }">
                    {{ !item.type ? "Жалоба" : "Вопрос" }}
                  </div>
                </div>
              </div>
              <div
                class="user-privilege"
                :class="{ [item.privilege]: item.privilege }"
                v-if="item.privilege"
              >
                {{
                  item.privilege === "vip-plus"
                    ? item.privilege.replace("-plus", "+")
                    : item.privilege
                }}
              </div>
              <img
                :src="require('@/assets/reps-arrow.svg')"
                class="arrow-logo"
                :class="{ active: myRepsChat === index }"
              />
            </div>
            <div class="chat" :class="{ active: myRepsChat === index }">
              <div class="history">
                <div
                  class="message"
                  :class="{ admin: item.admin }"
                  v-for="(item, index) in item.history"
                  :key="index"
                >
                  <div class="ava">
                    <img :src="item.avaUrl" />
                    <div class="online"></div>
                  </div>
                  <div class="data">
                    <div class="name">
                      {{ item.firstName + " " + item.lastName }}
                    </div>
                    <div class="text">
                      {{ item.text }}
                    </div>
                    <div class="timing">
                      {{ millisecondsToTimeString(item.time) }}
                    </div>
                  </div>
                </div>
              </div>
              <div class="write-message">
                <input type="text" placeholder="Напишите что-нибудь..." />
                <div class="send">
                  <img :src="require('@/assets/myReps-arrow.svg')" />
                </div>
                <div class="close">Закрыть обращение</div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
          commands: [
            {
              command: "mute",
              title: "Выдать мут игроку",
              type: "l",
            },
            {
              command: "kick",
              title: "Кикнуть игрока",
              type: "m",
            },
          ],
        },
        news: {
          firstName: "John",
          lastName: "Dorian",
          rangTitle: "Главный администратор",
          avaUrl: "/news-ava.png",
          timestamp: 1611529444189,
          message:
            "Уважаемые коллеги, завтра будет собрание администраторов в дискорде, быть всем и каждому. Cобрание будет в канале ‘администраторы сервера’ в 18:30 по московскому времени.",
        },
        reps: [
          {
            time: 1611771069162,
            firstName: "Romario",
            lastName: "Richardson",
            id: 456,
            accId: 1999,
            privilege: "vip", // vip, vip-plus, vip-pro, media
            text: "Как угнать машину?",
            checkingAdmin: false,
            type: true, // false - report, true - question
            closed: false,
            history: [],
          },
          {
            time: 1611772492677,
            firstName: "Stephan",
            lastName: "Carlson",
            id: 124,
            accId: 1977,
            privilege: "vip-plus", // vip, vip-plus, vip-pro, media
            text: "Админы плохие!",
            checkingAdmin: "Max Korzh",
            type: false, // false - report, true - question
            closed: true,
            history: [
              {
                time: 1611772492677,
                firstName: "Romario",
                lastName: "Richardson",
                avaUrl: "/header-ava.png",
                text: "Драсте, такой вопрос возник, как мне забанить админа?",
                admin: false,
              },
              {
                time: 1611772644444,
                firstName: "Max",
                lastName: "Korzh",
                avaUrl: "/news-ava.png",
                text:
                  "Сделайте сальто и прокричите ник администратора, досвидания",
                admin: true,
              },
            ],
          },
          {
            time: 1611772492677,
            firstName: "Joseph",
            lastName: "Defiano",
            id: 77,
            accId: 1114,
            privilege: false, // vip, vip-plus, vip-pro, media
            text: "Как открыть тачку?",
            checkingAdmin: "Max Korzh",
            type: true, // false - report, true - question
            closed: false,
          },
        ],
        myReps: [
          {
            time: 1611772492677,
            firstName: "Joseph",
            lastName: "Defiano",
            id: 77,
            accId: 1114,
            privilege: false, // vip, vip-plus, vip-pro, media
            text: "Как открыть тачку?",
            checkingAdmin: "Max Korzh",
            type: true, // false - report, true - question
            closed: false,
            history: [
              {
                time: 1611772492677,
                firstName: "Romario",
                lastName: "Richardson",
                avaUrl: "/header-ava.png",
                text: "Ну дык как ёмаё",
                admin: false,
              },
              {
                time: 1611772644444,
                firstName: "Max",
                lastName: "Korzh",
                avaUrl: "/news-ava.png",
                text: "Ну там оч изи крч, смари",
                admin: true,
              },
              {
                time: 1611773044444,
                firstName: "Max",
                lastName: "Korzh",
                avaUrl: "/news-ava.png",
                text: "*балдежные рассуждения*",
                admin: true,
              },
            ],
          },
        ],
      },
      repsChat: null,
      myRepsChat: null,
      modal: false,
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
  methods: {
    afkTime(milliseconds) {
      let past = new Date(milliseconds);
      let present = new Date();
      return Math.ceil(Math.abs(present.getTime() - past.getTime()) / 1000);
    },
    millisecondsToTimeString(timestamp) {
      return new Date(timestamp).toLocaleTimeString("en-GB");
    },
    openRepsChat(index) {
      if (this.repsChat !== null) return (this.repsChat = null);
      this.repsChat = index;
    },
    openMyRepsChat(index) {
      if (this.myRepsChat !== null) return (this.myRepsChat = null);
      this.myRepsChat = index;
    },
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
        let percent = Math.ceil((el.value * 100) / 43200);
        if (percent > 100) return 100;
        return percent;
      });
    },
    millisecondsToDateString() {
      return new Date(this.FETCHDATA.news.timestamp)
        .toLocaleString("en-GB")
        .replaceAll("/", ".")
        .replace(",", " /");
    },
    millisecondsToTimeStringArray() {
      return this.FETCHDATA.reps.map((el) => {
        return new Date(el.time).toLocaleTimeString("en-GB");
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

    & > .statistics {
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
        margin-bottom: 1.40625vw;

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

      .news {
        .title {
          margin-bottom: 0.520833vw;
        }

        .main {
          box-sizing: border-box;
          padding: 1.0416666667vw 1.5625vw;
          display: flex;
          background: linear-gradient(
            180deg,
            rgba(18, 18, 25, 0.85) 0%,
            rgba(18, 18, 26, 0.85) 100%
          );
          border-radius: 0.20833vw;

          .ava {
            align-self: flex-start;
            padding: 0.2083333333vw;
            border-radius: 50%;
            background: linear-gradient(180deg, #c41e37 0%, #fe0026 100%);
            filter: drop-shadow(0px 0px 0.625vw rgba(255, 31, 0, 0.49));

            img {
              display: block;
              width: 2.65625vw;
              height: 2.65625vw;
            }
          }

          .container {
            box-sizing: border-box;
            padding-top: 0.2604166667vw;
            flex-grow: 1;
            margin-left: 1.0416666667vw;

            .info {
              display: flex;
              justify-content: space-between;

              .user {
                .rang-title {
                  background: linear-gradient(90deg, #c41e37 0%, #fe0026 100%);
                  background-clip: text;
                  -webkit-text-fill-color: transparent;
                  color: #0b2349;
                }
              }

              .timestamp {
                color: rgba(255, 255, 255, 0.15);
              }
            }

            .message {
              box-sizing: border-box;
              padding-left: 0.4166666667vw;
              margin-top: 1.0416666667vw;
              color: rgba(255, 255, 255, 0.7);
              position: relative;

              &::before {
                content: "";
                width: 0.2083333333vw;
                height: 100%;
                background: linear-gradient(
                  180deg,
                  #ff1f00 0%,
                  #ff1f00 0.01%,
                  #c41e37 100%
                );
                position: absolute;
                top: 0;
                left: 0;
              }
            }
          }
        }
      }
    }

    & > .help {
      width: 50.3645833333vw;

      & > .title {
        margin-bottom: 0.520833vw;
      }

      .list {
        box-sizing: border-box;
        max-height: 45.1041666667vw;
        overflow-y: auto;

        &::-webkit-scrollbar {
          width: 0.15625vw;

          &-thumb {
            background: rgba(255, 255, 255, 0.48);
          }

          &-track {
            background: rgba(255, 255, 255, 0.08);
          }
        }

        .item {
          display: inline-block;
          border: 0.0520833333vw solid rgba(255, 255, 255, 0.14);
          border-radius: 0.2083333333vw;
          width: 14.375vw;
          line-height: 2.8645833333vw;
          text-align: center;
          margin-bottom: 0.8333333333vw;
          margin-right: 2.96875vw;

          &:nth-child(3n + 3) {
            margin-right: 0.6770833333vw;
          }

          &:hover {
            color: rgba(21, 21, 21, 0.9);
            background-color: #fff;
            box-shadow: 0px 0px 0.3125vw rgba(255, 255, 255, 0.75);
          }
        }
      }
    }

    .reps,
    .my-reps {
      width: 51.0416666667vw;

      & > .title {
        padding-left: 0.5208333333vw;
        margin-bottom: 0.520833vw;
      }

      .list {
        box-sizing: border-box;
        padding-left: 0.5208333333vw;
        max-height: 48vw;
        overflow-y: auto;

        &::-webkit-scrollbar {
          width: 0.15625vw;

          &-thumb {
            background: rgba(255, 255, 255, 0.48);
          }

          &-track {
            background: rgba(255, 255, 255, 0.08);
          }
        }

        .item {
          margin-bottom: 0.5729166667vw;

          &:last-child {
            margin-bottom: 0;
          }

          .report {
            box-sizing: border-box;
            padding: 1.6145833333vw 1.0416666667vw;
            display: flex;
            justify-content: space-between;
            width: 49.53125vw;
            background: linear-gradient(
              180deg,
              rgba(18, 18, 25, 0.85) 0%,
              rgba(18, 18, 26, 0.85) 100%
            );
            border-radius: 0.2083333333vw;
            position: relative;

            .user-data {
              display: flex;
              width: 10.9375vw;
              align-items: center;

              .logo {
                width: 1.6666666667vw;
                height: 1.6666666667vw;
                margin-right: 0.3645833333vw;
              }

              .data {
                .timing {
                  color: rgba(255, 255, 255, 0.3);
                }

                .name {
                  font-size: 1.3333333333rem;
                }

                .ids {
                  color: rgba(255, 255, 255, 0.15);
                }
              }
            }

            .report-info {
              text-align: center;

              .report-afk {
                color: rgba(255, 255, 255, 0.3);
                margin-bottom: 0.3645833333vw;

                span {
                  color: #ff1f00;
                }
              }

              .report-text {
                color: rgba(255, 255, 255, 0.7);
                font-size: 1.1111111111rem;
              }
            }

            .report-status {
              align-self: center;
              width: 10.9375vw;
              position: relative;

              .check-row,
              .type-row {
                display: flex;
                justify-content: space-between;

                .title {
                  color: rgba(255, 255, 255, 0.15);
                }

                .check {
                  color: #8fff00;
                  text-shadow: 0px 0px 0.3125vw rgba(143, 255, 0, 0.5);

                  &.not-empty {
                    color: #fff;
                    text-shadow: 0px 0px 0.3125vw rgba(255, 255, 0, 0.5);
                  }
                }

                .type {
                  color: #ff1f00;
                  text-shadow: 0px 0px 0.3125vw rgba(255, 31, 0, 0.5);

                  &.question {
                    color: #ffe600;
                    text-shadow: 0px 0px 0.3125vw rgba(255, 230, 0, 0.5);
                  }
                }
              }

              .check-row {
                margin-bottom: 0.1041666667vw;
              }

              .btn {
                box-sizing: border-box;
                border: 0.0520833333vw solid rgba(255, 255, 255, 0.14);
                border-radius: 0.1041666667vw;
                width: 4.2708333333vw;
                line-height: 0.9375vw;
                text-align: center;
                color: rgba(255, 255, 255, 0.19);
                position: absolute;
                top: calc(100% + 0.625vw);
                right: 0;

                &.free:hover {
                  background-color: #ffffff;
                  border-color: #fff;
                  color: #000;
                  box-shadow: 0px 0px 0.1041666667vw rgba(255, 255, 255, 0.55);
                }
              }
            }

            .user-privilege {
              writing-mode: vertical-lr;
              border-radius: 0.2083333333vw;
              height: 2.96875vw;
              line-height: 0.9895833333vw;
              text-align: center;
              color: #000;
              font-weight: bold;
              position: absolute;
              top: 50%;
              left: 0;
              transform: translate(-50%, -50%) rotate(180deg);

              &.vip {
                background: #ebff00;
                box-shadow: 0px 0px 0.3125vw rgba(235, 255, 0, 0.5);

                &-plus {
                  background: #ffa843;
                  box-shadow: 0px 0px 0.3125vw rgba(255, 122, 0, 0.5);
                }

                &-pro {
                  background: #ff4343;
                  box-shadow: 0px 0px 0.3125vw rgba(255, 40, 40, 0.5);
                }
              }

              &.media {
                background: #fff;
                box-shadow: 0px 0px 0.3125vw rgba(255, 255, 0, 0.5);
              }
            }

            .arrow-logo {
              width: 1.0416666667vw;
              height: 0.625vw;
              position: absolute;
              bottom: 0.5208333333vw;
              left: 50%;
              transform: translateX(-50%);

              &.active {
                transform: translateX(-50%) rotate(180deg);
              }
            }
          }

          .chat {
            box-sizing: border-box;
            padding: 2.03125vw 1.7708333333vw;
            display: none;
            flex-direction: column;
            height: 38.8020833333vw;
            width: 49.53125vw;
            margin-top: 2.0833333333vw;
            background: linear-gradient(
              180deg,
              rgba(18, 18, 25, 0.85) 0%,
              rgba(18, 18, 26, 0.85) 100%
            );
            border-radius: 0.2083333333vw;

            &.active {
              display: flex;
            }

            .history {
              flex-grow: 1;
              width: 100%;
              overflow-y: auto;

              &::-webkit-scrollbar {
                width: 0;
              }

              .message {
                display: flex;
                margin-bottom: 3.6458333333vw;

                &:last-child {
                  margin-bottom: 0;
                }

                &.admin {
                  flex-direction: row-reverse;

                  .ava {
                    margin-right: 0;
                    margin-left: 0.6770833333vw;
                  }

                  .data {
                    .name {
                      color: #ff1f00;
                    }
                    .timing {
                      right: none;
                      left: 0;
                    }
                  }
                }

                .ava {
                  position: relative;
                  align-self: flex-end;
                  margin-right: 0.6770833333vw;

                  img {
                    width: 2.8125vw;
                    height: 2.8125vw;
                    border-radius: 50%;
                  }

                  .online {
                    width: 0.78125vw;
                    height: 0.78125vw;
                    border-radius: 50%;
                    background-color: #8fff00;
                    position: absolute;
                    bottom: 0;
                    right: 0.2083333333vw;
                  }
                }

                .data {
                  box-sizing: border-box;
                  padding: 0.78125vw;
                  max-width: 70%;
                  border-radius: 0.2083333333vw;
                  background-color: rgba(255, 255, 255, 0.03);
                  position: relative;

                  .name {
                    color: #00ff85;
                    margin-bottom: 0.2604166667vw;
                  }

                  .text {
                    font-size: 1.11rem;
                  }

                  .timing {
                    color: rgba(255, 255, 255, 0.15);
                    position: absolute;
                    top: calc(100% + 0.3645833333vw);
                    right: 0;
                  }
                }
              }
            }

            .write-message {
              width: 100%;
              position: relative;

              input {
                box-sizing: border-box;
                padding: 1.25vw 3.9583333333vw 1.25vw 1.4583333333vw;
                border: 0;
                border-radius: 0.2083333333vw;
                outline: 0;
                width: 100%;
                font-family: Bebas Neue;
                font-size: 1.11rem;
                color: #fff;
                background-color: rgba(255, 255, 255, 0.03);

                &::placeholder {
                  color: rgba(255, 255, 255, 0.25);
                }
              }

              .send {
                display: flex;
                justify-content: center;
                align-items: center;
                width: 2.3958333333vw;
                height: 1.9791666667vw;
                background: rgba(255, 255, 255, 0.05);
                border-radius: 0.2083333333vw;
                position: absolute;
                top: 50%;
                right: 0.78125vw;
                transform: translateY(-50%);

                img {
                  display: block;
                  width: 0.8854166667vw;
                  height: 1.0416666667vw;
                }
              }

              .close {
                color: rgba(255, 255, 255, 0.5);
                text-decoration: underline;
                position: absolute;
                top: calc(100% + 0.5208333333vw);
                right: 0;
              }
            }
          }
        }
      }
    }
  }

  .my-reps .list .item .report .report-info {
    align-self: center;
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
