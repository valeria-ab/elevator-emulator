<template>
  <div class="elevator">
    <div class="onTheWayTo" v-if="currentFloor < onTheWayTo">
      &#129045; {{ onTheWayTo }}
    </div>
    <div class="onTheWayTo" v-if="currentFloor > onTheWayTo">
      &#129047; {{ onTheWayTo }}
    </div>
  </div>
</template>

<script>

export default {
  name: 'elevator-component',
  props: {
    onTheWayTo: Number,
    currentFloor: Number,
    floors: Number,
  },
};
</script>

<style lang="scss" scoped>
.elevator {
  height: 19.9%;
  width: 100%;
  background-color: rgb(12, 215, 255);
  position: absolute;
  bottom: 0;
  display: flex;
  justify-content: center;
}

.onTheWayTo {
  margin-top: 10px;
  border-radius: 4px;
  width: 50px;
  height: 30px;
  background-color: rgba(43, 73, 43, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}
</style>
