<template>
  <div class="elevator-emulator">
    <LiftShaft :floors="config.floors"/>
    <LobbyFloors :floors="config.floors"/>
  </div>
</template>

<script>
import LiftShaft from '@/components/LiftShaft.vue';
import LobbyFloors from '@/components/LobbyFloors.vue';

export default {
  name: 'App',
  components: { LiftShaft, LobbyFloors },
  data() {
    return {
      config: {
        floors: 5,
        shafts: 1,
      },
    };
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
  background: linear-gradient(#c1c1c1 0.5%, #ffffff 0.5%);
  background-size: 100% 20%;
  border-bottom: 1px #c1c1c1 solid;
  display: flex;
}

</style>
