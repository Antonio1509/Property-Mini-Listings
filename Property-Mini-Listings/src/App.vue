<template>
  <div id="app" class="app-container">
    <AppHeader :totalActive="totalActiveListings" />

    <FilterBar 
      :searchQuery="searchQuery" 
      :sortBy="sortBy"
      @update:searchQuery="searchQuery = $event"
      @update:sortBy="sortBy = $event"
    />

    <main class="property-grid">
      <PropertyCard 
        v-for="item in filteredAndSortedProperties" 
        :key="item.id"
        :property="item"
        :isBookmarked="bookmarkedIds.includes(item.id)"
        @toggle-bookmark="toggleBookmark"
      />
    </main>

    <div v-if="filteredAndSortedProperties.length === 0" class="empty-state">
      <p>No properties match your search criteria. Try looking somewhere else!</p>
    </div>
  </div>
</template>

<script>
import AppHeader from './components/Appheader.vue';
import FilterBar from './components/FilterBar.vue';
import PropertyCard from './components/PropertyCard.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    FilterBar,
    PropertyCard
  },
  data() {
    return {
      searchQuery: '',
      sortBy: 'default',
      bookmarkedIds: [],
      properties: [
        {
          id: 1,
          title: "Modern Sea-View Apartment",
          location: "Camps Bay, Cape Town",
          price: 17000,
          type: "Apartment",
          image: "https://fjbproperty.co.za/Images1/715873_1.jpg",
          available: false
        },
        {
          id: 2,
          title: "Cozy Mountain Loft",
          location: "Gardens, Cape Town",
          price: 16500,
          type: "Loft",
          image: "https://theharri.co.za/wp-content/uploads/2019/11/Layer-1.jpg",
          available: true
        },
        {
          id: 3,
          title: "Luxury Beachfront Villa",
          location: "Clifton, Cape Town",
          price: 45000,
          type: "Villa",
          image: "https://www.vacations.capetown/wp-content/uploads/2024/01/008-Bond-Villa-Camps-Bay-SAOTA-6.jpg",
          available: true
        },
        {
          id: 4,
          title: "Charming Heritage Cottage",
          location: "Clifton, Cape Town",
          price: 9000,
          type: "Cottage",
          image: "https://images.pp.co.za/listing/11852839/VPsGIpoRSvii5XEEupTMU1/600/450/contain/jpegorpng",
          available: true
        },
        {
          id: 5,
          title: "Urban Studio Apartment",
          location: "Green Point, Cape Town",
          price: 14500,
          type: "Apartment",
          image: "https://www.myroof.co.za/prop_static/MR074667/p/b/171767.jpg",
          available: true
        },
        {
          id: 6,
          title: "Guest House",
          location: "Milnerton, Cape Town",
          price: 13200,
          type: "Guest House",
          image: "https://cf.bstatic.com/xdata/images/hotel/max1024x768/683045101.jpg?k=d77e2d878786973594865238ef01ef8c31287c2521dd669eb85a96f487a1f2a0&o=",
          available: true
        },
        {
          id: 7,
          title: "Luxury Villa",
          location: "Constantia, Cape Town",
          price: 30000,
          type: "Villa",
          image: "https://theluxurytravelbook.com/wp-content/uploads/2023/11/luxury-villa-rental-south-africa-cape-town-Villa-Pagasvlei-34.jpg",
          available: false
        },
        {
          id: 8,
          title: "Small Home",
          location: "Delft, Cape Town",
          price: 3000,
          type: "House",
          image: "https://www.myroof.co.za/prop_static/MR110258/p/s/353854.JPG",
          available: true
        }
      ]
    };
  },
  computed: {
    totalActiveListings() {
      return this.properties.filter(p => p.available).length;
    },
    filteredAndSortedProperties() {
      let result = this.properties.filter(property => {
        return property.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
               property.location.toLowerCase().includes(this.searchQuery.toLowerCase());
      });

      if (this.sortBy === 'low-high') {
        return [...result].sort((a, b) => a.price - b.price);
      } else if (this.sortBy === 'high-low') {
        return [...result].sort((a, b) => b.price - a.price);
      }

      return result;
    }
  },
  methods: {
    toggleBookmark(id) {
      if (this.bookmarkedIds.includes(id)) {
        this.bookmarkedIds = this.bookmarkedIds.filter(bid => bid !== id);
      } else {
        this.bookmarkedIds.push(id);
      }
      localStorage.setItem('propertyBookmarks', JSON.stringify(this.bookmarkedIds));
    }
  },
  mounted() {
    const saved = localStorage.getItem('propertyBookmarks');
    if (saved) {
      this.bookmarkedIds = JSON.parse(saved);
    }
  }
};
</script>

<style>
.app-container {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  color: #333;
}

.property-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 25px;
  width: 100%;
}

.empty-state {
  text-align: center;
  padding: 40px;
  background-color: #f9f9f9;
  border-radius: 8px;
  color: #7f8c8d;
  grid-column: 1 / -1;
}
</style>