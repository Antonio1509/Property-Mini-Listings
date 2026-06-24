<template>
  <div class="property-card" :class="{ 'unavailable-card': !property.available }">
    <div v-if="!property.available" class="ribbon-unavailable">
      Not Available
    </div>

    <div class="image-wrapper">
      <img :src="property.image" :alt="property.title" class="property-image" />
    </div>

    <div class="property-details">
      <span class="property-type">{{ property.type || 'Property' }}</span>
      <h3 class="property-title">{{ property.title }}</h3>
      <p class="property-location">📍 {{ property.location }}</p>
      <p class="property-price"><strong>R {{ property.price }}</strong> / Month</p>
      
      <div class="card-actions">
        <button 
          @click="$emit('toggle-bookmark', property.id)" 
          class="btn-bookmark"
          :class="{ 'is-bookmarked': isBookmarked }"
        >
          {{ isBookmarked ? 'Bookmarked' : 'Bookmark' }}
        </button>
        <button :disabled="!property.available" class="btn-contact">
          Contact Agent
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    property: {
      type: Object,
      required: true
    },
    isBookmarked: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.property-card {
  border: 1px solid #eee;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  background: white;
  position: relative;
  display: flex;
  flex-direction: column;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.property-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.12);
  border-color: #3498db;
}

.image-wrapper {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.property-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.property-card:hover .property-image {
  transform: scale(1.06);
}

.unavailable-card {
  opacity: 0.6;
}

.unavailable-card:hover {
  transform: none;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  border-color: #eee;
}

.ribbon-unavailable {
  position: absolute;
  top: 15px;
  left: 15px;
  background-color: #e74c3c;
  color: white;
  padding: 4px 10px;
  font-size: 0.75rem;
  font-weight: bold;
  border-radius: 4px;
  z-index: 10;
}

.property-details {
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.property-type {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #95a5a6;
  font-weight: bold;
}

.property-title {
  margin: 5px 0;
  font-size: 1.15rem;
  color: #2c3e50;
}

.property-location {
  font-size: 0.9rem;
  color: #7f8c8d;
  margin-bottom: 15px;
}

.property-price {
  font-size: 1.1rem;
  margin-bottom: 15px;
  margin-top: auto;
}

.card-actions {
  display: flex;
  gap: 10px;
}

button {
  padding: 8px 12px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.85rem;
  flex: 1;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

button:active {
  transform: scale(0.97);
}

.btn-bookmark {
  background-color: #f8f9fa;
  border: 1px solid #ddd;
  color: #555;
}

.btn-bookmark:hover {
  background-color: #f1f2f6;
}

.btn-bookmark.is-bookmarked {
  background-color: #ffeef0;
  border-color: #ffb3ba;
  color: #e74c3c;
}

.btn-bookmark.is-bookmarked:hover {
  background-color: #ffd6da;
}

.btn-contact {
  background-color: #2ecc71;
  color: white;
}

.btn-contact:hover:not(:disabled) {
  background-color: #27ae60;
}

.btn-contact:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>