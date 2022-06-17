<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: 'MessageComp',
  props: {
    message: {
      type: String,
      default: '',
      required: true
    }
  },
}
</script>

<style scoped>
.message {
  text-align: center;
  margin-bottom: 10px;
  font-weight: 400;
  font-style: italic;
  color: rgb(163, 17, 17);
}
</style>
