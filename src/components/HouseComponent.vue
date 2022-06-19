<template>
  <div class="house">
    <div class="elevator-shaft">
      <FloorComponent
          v-for="fl in floorNum"
          :key="'floor - ' + fl"
      />
      <ElevatorComponent
          id="elevator"
          ref="elevator"
          class="elevator-position"
          :door-open="doorOpen"
      >
        <IndicationComponent
            :floor="currentFloor"
            :going-up="goingUp"
            :going-down="goingDown"
        />
      </ElevatorComponent>
    </div>
    <div class="floors">
      <FloorComponent
          v-for="fl in floorNum"
          :key="'floor - ' + fl"
      >
        <template #floor-header>
          <FloorNumberComponent
              :floor-number="floorNum - fl + 1"
          />
        </template>
        <template #floor-content>
          <PanelComponent
              :floor-number="floorNum - fl + 1"
              :is-active-request="this.queue.includes(floorNum - fl + 1)"
              :is-double-request="this.queueDouble.includes(floorNum - fl + 1)"
              @get-elevator="floorRequest"
          />
        </template>
      </FloorComponent>
    </div>
  </div>
</template>

<script>
import FloorComponent from '@/components/FloorComponent.vue';
import PanelComponent from '@/components/PanelComponent.vue';
import FloorNumberComponent from '@/components/FloorNumberComponent.vue';
import ElevatorComponent from '@/components/ElevatorComponent.vue';
import IndicationComponent from '@/components/IndicationComponent.vue';

export default {
  name: 'HouseComponent',
  components: {
    IndicationComponent,
    ElevatorComponent,
    FloorNumberComponent,
    PanelComponent,
    FloorComponent,
  },
  data() {
    return {
      floorNum: 5,
      currentFloor: 1,
      doorOpen: false,
      goingUp: false,
      goingDown: false,
      queue: [],
      queueDouble: [],
    };
  },
  computed: {
    idle() {
      return !(this.goingUp || this.goingDown);
    },
  },
  methods: {
    floorRequest(floor) {
      if (!this.queue.includes(floor) && !(this.currentFloor === floor && this.idle)) {
        this.queue.push(floor);
      } else if (this.queue.includes(floor) && !this.queueDouble.includes(floor)) {
        this.queueDouble.push(floor);
      }
    },
  },
};
</script>

<style scoped>
.house {
  display: flex;
  align-items: center;
  min-height: 100vh;
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
}

.elevator-shaft {
  position: relative;
  flex: 0 1 200px;
}

.elevator-position {
  position: absolute;
  bottom: 25px;
  left: 50%;
  transform: translateX(-50%);
}

.floors {
  flex: 1 1 auto;
}
</style>
