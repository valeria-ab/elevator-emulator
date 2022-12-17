<template>
  <div class="lift-shaft">
    <Elevator :current-floor="elevatorCallQueue[0]"
              :on-the-way-to="elevatorCallQueue[1]"
              :floors="floors"
              :elevator-call-queue="elevatorCallQueue"
              @delete-floor="this.deleteFloor"
    />
  </div>
</template>

<script>
import Elevator from '@/components/Elevator.vue';

export default {
  name: 'lift-shaft',
  components: { Elevator },
  props: {
    floors: Number,
    elevatorCallQueue: Array,
  },
  methods: {
    deleteFloor() {
      this.$emit('delete-floor');
    },
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
