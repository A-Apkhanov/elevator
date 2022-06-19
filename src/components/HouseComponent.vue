<template>
  <div class="house">
    <div class="elevator-shaft">
      <FloorComponent
        v-for="fl in 10"
        :key="'floor - ' + fl"
      />
      <ElevatorComponent
        id="elevator"
        ref="elevator"
        class="elevator-position"
      >
        <IndicationComponent />
      </ElevatorComponent>
    </div>
    <div class="floors">
      <FloorComponent
        v-for="fl in 10"
        :key="'floor - ' + fl"
      >
        <template #floor-header>
          <FloorNumberComponent />
        </template>
        <template #floor-content>
          <PanelComponent />
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
