<template>
  <header class="app-header">
    <h1>Homes & Beyond</h1>
    <p class="subtitle">Short-term rentals in Cape Town</p>
    <span class="badge count-badge">
      {{ totalActive }} Active Listings
    </span>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    totalActive: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.app-header {
  text-align: center;
  margin-bottom: 40px;
}
.app-header h1 {
  margin: 0;
  color: #2c3e50;
  font-size: 2.5rem;
}
.subtitle {
  color: #7f8c8d;
  margin: 5px 0 15px 0;
}
.badge {
  background-color: #3498db;
  color: white;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 0.85rem;
}
</style>