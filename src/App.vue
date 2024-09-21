<template>
  <div id="app">
    <header>
      <h1>Temporizador</h1>
    </header>
    <TimerComponent />
  </div>
</template>

<script>
import TimerComponent from './components/TimerComponent.vue';

export default {
  name: 'App',
  components: {
    TimerComponent
  }
};
</script>

<style>
@import './assets/style.css';
</style>
