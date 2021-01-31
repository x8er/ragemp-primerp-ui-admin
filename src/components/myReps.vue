<template>
  <div class="reps">
    <div class="title">Взаимодействие с репортами</div>
    <div class="list">
      <Report
        class="item"
        v-for="(item, index) in myReps"
        :key="index"
        :data="item"
        type="myReps"
      />
    </div>
  </div>
</template>

<script>
import Report from "@/components/report.vue";

export default {
  name: "MyReps",
  data() {
    return {
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
    };
  },
  components: {
    Report,
  },
};
</script>

<style lang="scss">
.reps {
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
    }
  }
}
</style>