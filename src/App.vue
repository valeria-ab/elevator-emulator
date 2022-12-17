<template>
  <div class="elevator-emulator">
    <div class="elevator-emulator__container">
      <LiftShaft :floors="config.floors"
                 :elevatorCallQueue="elevatorCallQueue"
                 @delete-floor="deleteFloorFromElevatorCallQueue"
      />
      <LobbyFloors :floors="config.floors"
                   @set-floor="addNewCallToElevatorCallQueue"
                   :elevator-call-queue="elevatorCallQueue"
      />
    </div>
  </div>
</template>

<script>
import LiftShaft from '@/components/LiftShaft.vue';
import LobbyFloors from '@/components/LobbyFloors.vue';

export default {
  name: 'App',
  components: {LiftShaft, LobbyFloors},
  data() {
    return {
      config: {
        floors: 5,
        shafts: 1,
      },
      elevatorCallQueue: [1],
    };
  },
  methods: {
    addNewCallToElevatorCallQueue(floor) {
      this.elevatorCallQueue = [...this.elevatorCallQueue, floor];
    },
    deleteFloorFromElevatorCallQueue() {
      this.elevatorCallQueue = this.elevatorCallQueue.filter((_, index) => index !== 0);
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

ul {
  margin: 0;
  padding: 0;
}

li {
  list-style: none;
}

.elevator-emulator {
  width: 100%;
  height: 100vh;
  padding: 8px 15px;

  &__container {
    height: 100%;
    width: 100%;
    background: linear-gradient(#c1c1c1 0.5%, #ffffff 0.5%);
    background-size: 100% 20%;
    border-bottom: 1px #c1c1c1 solid;
    display: flex;
  }
}

</style>
