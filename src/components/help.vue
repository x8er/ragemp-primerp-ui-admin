<template>
  <div class="help">
    <div class="title">Команды для взаимодействия с сервером</div>
    <div class="list">
      <div
        class="item"
        v-for="(item, index) in commands"
        :key="index"
        @click="$emit('modal', { ...item })"
      >
        {{ item.title }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Help",
  data() {
    return {
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
    };
  },
};
</script>

<style lang="scss">
.help {
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
</style>