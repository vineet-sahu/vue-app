<template>
  <div class="app">
    <!-- Header -->
    <header class="header">
      <h1>🎬 Vue Movie Finder</h1>

      <!-- Search Bar -->
      <div class="search-bar">
        <input
          v-model="searchQuery"
          @keyup.enter="searchMovies"
          placeholder="Search for movies..."
          class="search-input"
        />
        <button @click="searchMovies" :disabled="loading" class="search-btn">
          {{ loading ? 'Searching...' : 'Search' }}
        </button>
      </div>
    </header>

    <!-- Main Content -->
    <main class="container">
      <!-- Error Message -->
      <div v-if="error" class="error">{{ error }}</div>

      <!-- Loading State -->
      <div v-if="loading" class="loading">Searching movies...</div>

      <!-- Movie Details Cards -->
      <div v-if="!loading && movies.length > 0" class="movie-details-grid">
        <div v-for="movie in movies" :key="movie['#IMDB_ID']" class="movie-box">
          <div class="poster-container">
            <img
              v-if="movie['#IMG_POSTER']"
              :src="movie['#IMG_POSTER']"
              :alt="movie['#TITLE']"
              class="poster"
            />
            <div v-else class="poster-placeholder">🎬</div>
          </div>

          <div class="info">
            <h2>{{ movie['#TITLE'] }}</h2>
            <p><strong>Year:</strong> {{ movie['#YEAR'] }}</p>
            <p><strong>Actors:</strong> {{ movie['#ACTORS'] || 'N/A' }}</p>
            <p><strong>Also Known As:</strong> {{ movie['#AKA'] || 'N/A' }}</p>
            <p><strong>Rank:</strong> {{ movie['#RANK'] }}</p>
            <p>
              <strong>IMDb:</strong>
              <a :href="movie['#IMDB_URL']" target="_blank">
                {{ movie['#IMDB_ID'] }}
              </a>
            </p>
          </div>
        </div>
      </div>

      <!-- Empty State -->
      <div v-if="!loading && !error && searchQuery && movies.length === 0" class="empty">
        No movies found
      </div>
    </main>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      searchQuery: '',
      movies: [] as any[],
      loading: false,
      error: '',
    }
  },
  methods: {
    async searchMovies() {
      if (!this.searchQuery.trim()) return
      this.loading = true
      this.error = ''
      this.movies = []

      try {
        const response = await fetch(
          `https://imdb.iamidiotareyoutoo.com/search?q=${encodeURIComponent(this.searchQuery)}&tt=&lsn=1&v=1`,
        )
        const data = await response.json()

        if (data.ok && Array.isArray(data.description)) {
          this.movies = data.description
        } else {
          this.error = 'No movies found'
        }
      } catch (err) {
        this.error = 'Failed to fetch movies. Please try again.'
      } finally {
        this.loading = false
      }
    },
  },
}
</script>

<style scoped>
.app {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.header {
  background: rgba(0, 0, 0, 0.3);
  padding: 2rem;
  border-bottom: 2px solid rgba(255, 255, 255, 0.1);
  text-align: center;
}

h1 {
  color: white;
  margin-bottom: 1rem;
  font-size: 2rem;
}

.search-bar {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  max-width: 600px;
  margin: 0 auto;
}

.search-input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  font-size: 1rem;
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.search-btn {
  padding: 0.75rem 1.5rem;
  background: #fff;
  color: #667eea;
  border: none;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

.search-btn:hover {
  background: #f0f0f0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.error {
  background: #ff4444;
  color: white;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.loading,
.empty {
  text-align: center;
  color: white;
  font-size: 1.2rem;
  padding: 3rem;
}

/* 🎬 Movie Details Layout */
.movie-details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

.movie-box {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  overflow: hidden;
  transition: transform 0.2s;
  padding-bottom: 1rem;
}

.movie-box:hover {
  transform: scale(1.02);
}

.poster-container {
  width: 100%;
  aspect-ratio: 2/3;
  background: rgba(0, 0, 0, 0.3);
}

.poster {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.poster-placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  height: 100%;
}

.info {
  padding: 1rem;
  color: white;
}

.info h2 {
  margin: 0 0 0.5rem 0;
  font-size: 1.2rem;
  color: #fff;
}

.info p {
  margin: 0.3rem 0;
  font-size: 0.9rem;
  line-height: 1.4;
}

a {
  color: #ffd700;
  text-decoration: underline;
}
</style>
