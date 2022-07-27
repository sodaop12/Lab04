<template>
  <p>Airline name: {{ event.airline[0].name }}</p>
  <p>Airline slogan: {{ event.airline[0].slogan }}</p>
  <p>head_quaters: {{ event.airline[0].head_quaters }}</p>
</template>

<script>
export default {
  props: ['event']
}
</script>
