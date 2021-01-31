<template>
  <div class="reps">
    <div class="title">Взаимодействие с репортами</div>
    <div class="list">
      <Report
        class="item"
        v-for="(item, index) in reps"
        :key="index"
        :data="item"
        type="reps"
      />
    </div>
  </div>
</template>

<script>
import Report from "@/components/report.vue";

export default {
  name: "Reps",
  data() {
    return {
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