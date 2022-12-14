<template>
  <div class="lift-shaft">
    <Elevator :current-floor="1" :on-the-way-to="5" :floors="floors"/>
  </div>
</template>

<script>
import Elevator from '@/components/Elevator.vue';

export default {
  name: 'lift-shaft',
  components: { Elevator },
  props: {
    floors: Number,
  },
};
</script>

<style lang="scss" scoped>

.lift-shaft {
  height: 100%;
  width: 150px;
  border-left: 4px solid #bababa;
  border-right: 4px solid #bababa;
  margin-right: 20px;
  position: relative;
}

</style>
