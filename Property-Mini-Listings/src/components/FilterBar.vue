<template>
  <section class="controls-bar">
    <input 
      :value="searchQuery"
      @input="$emit('update:searchQuery', $event.target.value)" 
      type="text" 
      placeholder="Search by title or location..." 
      class="search-input"
    />

    <select 
      :value="sortBy" 
      @change="$emit('update:sortBy', $event.target.value)" 
      class="sort-select"
    >
      <option value="default">Sort by Price</option>
      <option value="low-high">Price: Low to High</option>
      <option value="high-low">Price: High to Low</option>
    </select>
  </section>
</template>

<script>
export default {
  name: 'FilterBar',
  props: {
    searchQuery: String,
    sortBy: String
  }
}
</script>

<style scoped>
.controls-bar {
  display: flex;
  gap: 15px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}
.search-input {
  flex: 1;
  min-width: 250px;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
}
.sort-select {
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
  background-color: white;
  cursor: pointer;
}
</style>