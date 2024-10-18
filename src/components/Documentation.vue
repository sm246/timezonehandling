<template>
  <div>
    <div class="page-wrapper">
      <!-- ******Header****** -->
      <header id="header" class="header">
        <div class="container">
          <div class="branding">
            <h1 class="logo">
              <a href="index.html">
                <span aria-hidden="true" class="fas fa-clock"></span>
                <span class="text-highlight"> TimeZone </span
                ><span class="text-bold">Handling</span>
              </a>
            </h1>
          </div>
          <!-- <div class="top-search-box">
            <form
              @submit.prevent="performSearch"
              class="form-inline search-form justify-content-center"
            >
              <input
                type="text"
                v-model="searchQuery"
                placeholder="Search..."
                name="search"
                class="form-control search-input"
              />

              <button type="submit" class="btn search-btn" value="Search">
                <i class="fas fa-search"></i>
              </button>
            </form>
            <div v-if="results.length">
              <h3>Search Results:</h3>
              <ul>
                <li v-for="result in results" :key="result.id">
                  {{ result.name }}
                </li>
              </ul>
            </div>
          </div> -->
          <!-- <div class="top-search-box">
            <form
              @submit.prevent="performSearch"
              class="form-inline search-form justify-content-center"
            >
              <input
                type="text"
                v-model="searchQuery"
                placeholder="Search..."
                name="search"
                class="form-control search-input"
              />

              <button type="submit" class="btn search-btn" value="Search">
                <i class="fas fa-search"></i>
              </button>
            </form>
            <div v-if="results.length">
              <h3>Search Results:</h3>
              <ul>
                <li v-for="(result, index) in results" :key="index">
                  {{ result }}
                </li>
              </ul>
            </div>
            <div v-else-if="searchQuery">
              <h3>No results found for "{{ searchQuery }}"</h3>
            </div>
          </div>-->
        </div>
      </header>
      <div class="doc-wrapper">
        <div class="container">
          <div class="doc-body row">
            <div class="doc-content col-md-9 col-12 order-1">
              <div class="content-inner">
                <introduction />
                <browser-timezone />
                <profile-timezone />
                <database-timezone />
                <background-timezone />
              </div>
            </div>
            <div class="doc-sidebar col-md-3 col-12 order-0 d-none d-md-flex">
              <div id="doc-nav" class="doc-nav">
                <nav id="doc-menu" class="nav doc-menu flex-column sticky">
                  <li class="nav-item">
                    <a class="nav-link scrollto" href="#introduction-section"
                      >Introduction</a
                    >
                  </li>
                  <li class="nav-item">
                    <a
                      class="nav-link scrollto"
                      href="#browser-timezone-section"
                    >
                      Browser’s Timezone</a
                    >
                  </li>

                  <li class="nav-item">
                    <a
                      class="nav-link scrollto"
                      href="#profile-timezone-section"
                    >
                      Profile Timezone</a
                    >
                  </li>
                  <li class="nav-item">
                    <a
                      class="nav-link scrollto"
                      href="#database-timezone-section"
                    >
                      Database Timezone</a
                    >
                  </li>
                  <li class="nav-item">
                    <a
                      class="nav-link scrollto"
                      href="#background-timezone-section"
                    >
                      Background Timezone</a
                    >
                  </li>
                </nav>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import "../assets/css/styles.css";
import "../assets/plugins/simplelightbox/simple-lightbox.min.css";
import "../assets/plugins/elegant_font/css/style.css";
import "../assets/plugins/prism/prism.css";
import "../assets/plugins/bootstrap/css/bootstrap.min.css";
import Introduction from "./Introduction.vue";
import BrowserTimezone from "./BrowserTimezone.vue";
import ProfileTimezone from "./ProfileTimezone.vue";
import DatabaseTimezone from "./DatabaseTimezone.vue";
import BackgroundTimezone from "./BackgroundTimezone.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Documentation",
  components: {
    Introduction,
    BrowserTimezone,
    ProfileTimezone,
    DatabaseTimezone,
    BackgroundTimezone
  },
  data() {
    return {
      searchQuery: "",
      results: []
    };
  },
  methods: {
    performSearch() {
      // Clear previous results
      this.results = [];

      // Get all text content from the body
      const bodyText = document.body.innerText;

      // Split the body text into words
      const words = bodyText.split(/\s+/);

      // Filter words that match the search query
      this.results = words.filter((word) =>
        word.toLowerCase().includes(this.searchQuery.toLowerCase())
      );

      // Optionally, you can also search for phrases or sentences
      // For example, you can search for sentences containing the query
      const sentences = bodyText.split(". ");
      const matchedSentences = sentences.filter((sentence) =>
        sentence.toLowerCase().includes(this.searchQuery.toLowerCase())
      );

      // Combine results from words and sentences if needed
      this.results = [...new Set([...this.results, ...matchedSentences])];
    }
  }
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
.language-markup {
  width: 100% !important;
}
.language-css {
  width: 100% !important;
}
.language-python {
  width: 100% !important;
}
</style>
<style>
.language-javascript {
  color: white !important;
  background-color: transparent;
}
.v-code-block--code-copy-button {
  right: 1rem !important;
  top: 1rem !important;
}
.doc-section {
  padding-top: 0px !important;
  padding-bottom: 0px !important;
  padding-left: 10px;
}
</style>
