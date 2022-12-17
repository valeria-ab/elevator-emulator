<template>
  <ul class="lobby-floors">
    <li
        :class="['lobby-floors__floor', `floor${floor + 1}`]"
        v-for="(floor, index) in floorButtons"
        :key="index"
    >
      <div>{{floor + 1}}</div>
      <button
          :class="['lobby-floors__floor-button',
          {'active': elevatorCallQueue.slice(1).includes(floor + 1)}]"
          type="button"
          @click="onFloorButtonClick(floor + 1)"
      />
    </li>
  </ul>
</template>

<script>

export default {
  name: 'lobby-floors',
  props: {
    floors: Number,
    elevatorCallQueue: Array,
  },
  data() {
    return {
      floorButtons: [],
    };
  },
  methods: {
    onFloorButtonClick(floor) {
      if (this.elevatorCallQueue[this.elevatorCallQueue.length - 1] !== floor) {
        this.$emit('set-floor', floor);
      }
    },
  },
  created() {
    this.floorButtons = Array.from(Array(this.floors).keys());
  },
};
</script>

<style lang="scss" scoped>
.lobby-floors {
  height: 100%;
  width: 80px;
  position: relative;

  .floor1 {
    top: 80%
  }

  .floor2 {
    top: 60%
  }

  .floor3 {
    top: 40%
  }

  .floor4 {
    top: 20%
  }

  .floor5 {
    top: 0;
  }

  &__floor {
    position: absolute;
    padding-top: 10px;
    height: 20%;

    &-button {
      margin-top: 10px;
      width: 30px;
      height: 30px;
      border: 1px solid #2CA5C1FF;
      background-color: inherit;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;

      &::before,
      &::after {
        content: '';
        border-radius: 100%;
      }

      &::before {
        width: 16px;
        height: 16px;
        border: 1px solid #2CA5C1FF;
      }

      &::after {
        position: absolute;
        width: 8px;
        height: 8px;
        background: #2CA5C1FF;
      }

    }
  }
}

.lobby-floors__floor-button.active {
  border: 1px solid #C12C42FF;

  &::before {
    border: 1px solid #C12C42FF;
  }

  &::after {
    background: #C12C42FF;
  }
}
</style>
