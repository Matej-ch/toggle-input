<template>
  <div id="app">
      <toggle-input
          label-enable-text='On'
          label-disable-text='Off'
          :default-state="0"
          :form-inputs="{modelid:'25',isEditable:1}" url='/path/to/update'/>

      <div style="width: 100%;padding: 30px"></div>

      <toggle-input
          label-enable-text='On'
          label-disable-text='Off'
          :default-state="1"
          :form-inputs="{modelid:'25',isEditable:1}" url='/path/to/update'/>

      <div style="width: 100%;padding: 30px"></div>

      <toggle-input
          label-enable-text='On'
          label-disable-text='Off'
          :default-state="1"
          size="lg"
          :form-inputs="{modelid:'25',isEditable:1}" url='/path/to/update'/>
  </div>
</template>

<script>
import ToggleInput from './components/ToggleInput.vue'

export default {
  name: 'App',
  components: {
    ToggleInput
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
