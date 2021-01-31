<template>
  <div class="statistics">
    <div class="lil-stats">
      <Stats type="online" />
      <Stats type="answer" />
      <Stats type="timing" />
    </div>
    <DetailedOnlineStats />
    <div class="news">
      <div class="title">Новости</div>
      <div class="main">
        <div class="ava">
          <img src="/news-ava.png" />
        </div>
        <div class="container">
          <div class="info">
            <div class="user">
              <div class="rang-title">{{ news.rangTitle }}</div>
              <div class="fullname">
                {{ news.firstName + " " + news.lastName }}
              </div>
            </div>
            <div class="timestamp">{{ millisecondsToDateString }}</div>
          </div>
          <div class="message">{{ news.message }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Stats from "@/components/stats.vue";
import DetailedOnlineStats from "@/components/detailed-online-stats.vue";

export default {
  name: "Statistics",
  data() {
    return {
      news: {
        firstName: "John",
        lastName: "Dorian",
        rangTitle: "Главный администратор",
        avaUrl: "/news-ava.png",
        timestamp: 1611529444189,
        message:
          "Уважаемые коллеги, завтра будет собрание администраторов в дискорде, быть всем и каждому. Cобрание будет в канале ‘администраторы сервера’ в 18:30 по московскому времени.",
      },
    };
  },
  computed: {
    millisecondsToDateString() {
      return new Date(this.news.timestamp)
        .toLocaleString("en-GB")
        .replaceAll("/", ".")
        .replace(",", " /");
    },
  },
  components: {
    Stats,
    DetailedOnlineStats,
  },
};
</script>

<style lang="scss">
.statistics {
  width: 49.53125vw;

  .lil-stats {
    display: flex;
    justify-content: space-between;
    width: inherit;
    margin-bottom: 1.40625vw;
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
</style>