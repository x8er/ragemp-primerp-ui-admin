<template>
  <div>
    <div class="report" @click="chat = !chat">
      <div class="user-data">
        <img :src="require('@/assets/reps-ava.svg')" class="logo" />
        <div class="data">
          <div class="timing">
            {{ millisecondsToTimeString(data.time) }}
          </div>
          <div class="name">
            {{ data.firstName + " " + data.lastName }}
          </div>
          <div class="ids">[{{ data.id }}], #{{ data.accId }}</div>
        </div>
      </div>
      <div class="report-info" :class="{ my: type === 'myReps' }">
        <div class="report-afk" v-if="type === 'reps'">
          Репорт без ответа <span>{{ afkTime(data.time) }}</span> сек.
        </div>
        <div class="report-text">{{ data.text }}</div>
      </div>
      <div class="report-status">
        <div class="check-row">
          <div class="title">Проверяет:</div>
          <div class="check" :class="{ 'not-empty': data.checkingAdmin }">
            {{ !data.checkingAdmin ? "Свободный тикет" : data.checkingAdmin }}
          </div>
        </div>
        <div class="type-row">
          <div class="title">Тип обращения:</div>
          <div class="type" :class="{ question: data.type }">
            {{ !data.type ? "Жалоба" : "Вопрос" }}
          </div>
        </div>
        <div
          class="btn"
          :class="{ free: !data.closed && !data.checkingAdmin }"
          v-if="type === 'reps'"
        >
          {{ !data.checkingAdmin && !data.closed ? "Забрать" : "" }}
          {{ data.checkingAdmin && !data.closed ? "Недоступно" : "" }}
          {{ data.checkingAdmin && data.closed ? "Закрыто" : "" }}
        </div>
      </div>
      <div
        class="user-privilege"
        :class="{ [data.privilege]: data.privilege }"
        v-if="data.privilege"
      >
        {{
          data.privilege === "vip-plus"
            ? data.privilege.replace("-plus", "+")
            : data.privilege
        }}
      </div>
      <img
        :src="require('@/assets/reps-arrow.svg')"
        class="arrow-logo"
        :class="{ active: chat }"
      />
    </div>
    <div class="chat" :class="{ active: chat }">
      <div class="history">
        <div
          class="message"
          :class="{ admin: item.admin }"
          v-for="(item, index) in data.history"
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
      <div class="write-message" v-if="type === 'myReps'">
        <input type="text" placeholder="Напишите что-нибудь..." />
        <div class="send">
          <img :src="require('@/assets/myReps-arrow.svg')" />
        </div>
        <div class="close">Закрыть обращение</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Report",
  props: ["data", "type"],
  data() {
    return {
      chat: false,
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
  },
};
</script>

<style lang="scss">
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

    &.my {
      align-self: center;
    }

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
</style>