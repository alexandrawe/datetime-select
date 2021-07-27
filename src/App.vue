<template>
  <div id="app" class="bg-blue-200 h-screen flex justify-center items-center">
    <appointment-duration-select></appointment-duration-select>
  </div>
</template>

<script>
import AppointmentDurationSelect from './components/AppointmentDurationSelect.vue'

export default {
  name: 'App',
  components: {
    AppointmentDurationSelect
  },
}
</script>