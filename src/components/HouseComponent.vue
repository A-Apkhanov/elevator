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
          :style="{ bottom: `${25 + (currentFloor - 1) * 205}px` }"
      >
        <IndicationComponent
            :floor="(doorOpen && currentFloor) || (queue[0] || currentFloor)"
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
      timer: null,
    };
  },
  mounted() {
    this.timer = setInterval(this.run, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
  computed: {
    idle() {
      return !(this.goingUp || this.goingDown);
    },
  },
  watch: {
    currentFloor(newCurrentFloor, oldCurrentFloor) {
      const difference = newCurrentFloor - oldCurrentFloor;
      const duration = 1000;
      const draw = (progress) => {
        this.$refs.elevator.$el.style.bottom = `${25 + (oldCurrentFloor - 1) * 205
        + difference * progress * 205}px`;
      };
      const timing = (timeFraction) => timeFraction;

      this.animate({ duration, timing, draw });
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

    stopBy() {
      if (this.timer) {
        clearInterval(this.timer);
      }
      this.doorOpen = true;
      this.goingDown = false;
      this.goingUp = false;
      setTimeout(() => {
        this.doorOpen = false;
        setTimeout(() => {
          this.timer = setInterval(this.run, 1000);
        }, 0);
      }, 3000);
    },

    changeDirection() {
      if (this.queue.length === 0) {
        this.goingDown = false;
        this.goingUp = false;
      } else if (this.currentFloor < this.queue[0]) {
        this.goingDown = false;
        this.goingUp = true;
      } else if (this.currentFloor > this.queue[0]) {
        this.goingDown = true;
        this.goingUp = false;
      }
    },

    removeFloor(floor) {
      const floorIndex = this.queue.indexOf(floor);
      const floorDoubleIndex = this.queueDouble.indexOf(floor);
      if (~floorIndex) {
        this.queue.splice(floorIndex, 1);
      }
      if (~floorDoubleIndex) {
        this.queueDouble.splice(floorDoubleIndex, 1);
      }
    },

    goUp() {
      if (this.goingUp) {
        if (this.currentFloor < this.floorNum) {
          this.currentFloor += 1;
        }
      }
    },

    goDown() {
      if (this.goingDown) {
        if (this.currentFloor > 1) {
          this.currentFloor -= 1;
        }
      }
    },

    goOn() {
      this.changeDirection();
      if (this.goingUp && this.currentFloor < this.floorNum) {
        this.goUp();
      } else if (this.goingDown && this.currentFloor > 1) {
        this.goDown();
      }
    },

    run() {
      let stopFlag = false;
      const floor = this.currentFloor;

      if (!this.idle) {
        if (floor === this.queue[0]) {
          this.removeFloor(floor);
          stopFlag = true;
        }

        if (stopFlag) {
          this.stopBy(floor);
        } else {
          this.goOn();
        }
      } else {
        this.goOn();
      }
    },

    animate({ timing, draw, duration }) {
      const start = performance.now();
      requestAnimationFrame(function animate(time) {
        let timeFraction = (time - start) / duration;
        if (timeFraction > 1) timeFraction = 1;
        const progress = timing(timeFraction);
        draw(progress);
        if (timeFraction < 1) {
          requestAnimationFrame(animate);
        }
      });
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
  left: 50%;
  transform: translateX(-50%);
}

.floors {
  flex: 1 1 auto;
}
</style>
