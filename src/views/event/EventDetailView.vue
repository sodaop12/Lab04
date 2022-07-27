<template>
  <p>Name: {{ event.name }}</p>
  <p>PassengerID: {{ event._id }}</p>
</template>

<script>
export default {
  props: ['event']
}
</script>
