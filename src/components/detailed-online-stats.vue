<template>
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
          v-for="(item, index) in week"
          :key="index"
        >
          <div class="day-name">{{ item.dayName }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailedOnlineStats",
  data() {
    return {
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
    };
  },
  computed: {
    secondToPercentArray() {
      return this.week.map((el) => {
        let percent = Math.ceil((el.value * 100) / 43200);
        if (percent > 100) return 100;
        return percent;
      });
    },
  },
};
</script>

<style lang="scss">
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
</style>