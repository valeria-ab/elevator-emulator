<template>
  <div class="elevator"
       :style="computedStyle"
  >
    <div class="on-the-way-to" v-if="currentFloor < onTheWayTo">
      &#129045; {{ onTheWayTo }}
    </div>
    <div class="on-the-way-to" v-if="currentFloor > onTheWayTo">
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
    elevatorCallQueue: Array,
  },
  data() {
    return {
      bottomValue: 0,
      opacity: 1,
      prevFloor: 0,
    };
  },
  computed: {
    oneFloorHeight() { return (1 / this.floors) * 100; },
    computedCurrentFloorHeight() {
      return (this.currentFloor * this.oneFloorHeight) - 20;
    },
    computedDistanceToDestination() {
      return Math.abs(this.onTheWayTo - this.currentFloor) * this.oneFloorHeight;
    },

    computedStyle() {
      if (this.bottomValue && (this.currentFloor < this.onTheWayTo)) {
        return `bottom: ${this.computedCurrentFloorHeight + this.bottomValue}%; opacity: ${this.opacity}`;
      }
      if (this.bottomValue && (this.currentFloor > this.onTheWayTo)) {
        return `bottom: ${this.computedCurrentFloorHeight - this.bottomValue}%; opacity: ${this.opacity}`;
      }
      return `bottom: ${this.computedCurrentFloorHeight}%; opacity: ${this.opacity}`;
    },
  },
  methods: {
    setStyle(distancePerIteration) {
      this.bottomValue += distancePerIteration;
    },
    setFlickering(value) {
      this.opacity = value;
    },
    moveElevator() {
      let start = Date.now();
      const distanceTime = Math.abs(this.onTheWayTo - this.currentFloor);
      let timer = setInterval(() => {

        let timePassed = Date.now() - start;

        if (timePassed >= distanceTime * 1000) {
          let startTimeFlickeringFunction = Date.now();
          let isOpacity = true;

          let flickering = setInterval(() => {
            let timeFlickeringFunctionPassed = Date.now() - startTimeFlickeringFunction;

            if (timeFlickeringFunctionPassed >= 3500) {
              this.bottomValue = 0;
              if (this.elevatorCallQueue.length > 1) {
                this.$emit('delete-floor');
              }

              clearInterval(flickering);
              return;
            }
            if (isOpacity) {
              this.setFlickering(0.5);
              isOpacity = false;
            } else {
              this.setFlickering(1);
              isOpacity = true;
            }
          }, 500);

          clearInterval(timer);
        }

        const distancePerIteration = this.computedDistanceToDestination
            / ((distanceTime * 1000) / 20);

        this.setStyle(distancePerIteration);
      }, 20);
    },
  },
  watch: {
    elevatorCallQueue(value) {
      if (this.prevFloor !== value[0] && value.length >= 2) {
        this.moveElevator();
      }
      if (value.length === 1) {
        this.prevFloor = 0;
      } else {
        // eslint-disable-next-line prefer-destructuring
        this.prevFloor = value[0];
      }
    },
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

.on-the-way-to {
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
