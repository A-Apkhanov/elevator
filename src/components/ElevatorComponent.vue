<template>
  <div
      class="elevator"
  >
    <p
        class="elevator-state"
        :class="[doorOpen ? 'open' : 'close']"
    >
      {{ doorOpen ? 'Open' : 'Close' }}
    </p>
    <slot/>
  </div>
</template>

<script>
export default {
  name: 'ElevatorComponent',
  props: {
    doorOpen: Boolean,
  },
};
</script>

<style scoped>
.elevator {
  width: 130px;
  height: 160px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  background-color: #0a9396;
  border-radius: 10px;
}

.elevator-state {
  display: inline-block;
  margin: 0;
  padding: 10px;
  font-size: 25px;
  font-weight: 700;
  text-transform: uppercase;
}

.close {
  color: #9b2226;
  border: 2px solid #9b2226;
  border-radius: 10px;
}

.open {
  color: #94d2bd;
  border: 2px solid #94d2bd;
  border-radius: 10px;
}
</style>
