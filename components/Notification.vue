<template>
  <div class="notification is-danger">
    {{ massage }}
  </div>
</template>

<script>
export default {
  name: 'Notification',
  props: ['massage']
}
</script>