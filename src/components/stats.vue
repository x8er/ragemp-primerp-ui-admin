<template>
  <div class="stats">
    <div class="title" v-if="type === 'online'">
      Статистика онлайна администратора
    </div>
    <div class="title" v-else-if="type === 'answer'">
      Статистика ответов администратора
    </div>
    <div class="title" v-else-if="type === 'timing'">
      Статистика времени ответа
    </div>
    <div class="main">
      <div class="name">
        <div class="dot"></div>
        <span v-if="type === 'online'">Часов</span>
        <span v-else-if="type === 'answer'">Репорты</span>
        <span v-else-if="type === 'timing'">В среднем</span>
      </div>
      <div class="value">
        {{ this[type][currentSort] }}
      </div>
      <div class="sort">
        <div
          class="item"
          :class="{ active: currentSort === 0 }"
          @click="currentSort = 0"
        >
          За день
        </div>
        <div
          class="item"
          :class="{ active: currentSort === 1 }"
          @click="currentSort = 1"
        >
          За неделю
        </div>
        <div
          class="item"
          :class="{ active: currentSort === 2 }"
          @click="currentSort = 2"
        >
          За месяц
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Stats",
  props: ["type"],
  data() {
    return {
      online: [8, 54, 454],
      answer: [1356, 10778, 32588],
      timing: [30, 42, 34],
      currentSort: 0,
    };
  },
};
</script>

<style lang="scss">
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
</style>