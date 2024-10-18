<template>
  <section id="browser-timezone-section" class="doc-section">
    <h2 class="section-title">Using Browser’s Timezone (Frontend)</h2>
    <div class="section-block">
      <p>
        <a href="https://www.timeanddate.com/" target="_blank">Time and Date</a>
        is a comprehensive resource for time zone information, including current
        times, time zone conversions, and daylight saving time changes. You can
        also
        <a
          href="https://www.timeanddate.com/worldclock/converter.html"
          target="_blank"
          >use their time zone converter</a
        >
        to easily convert times between different zones.
      </p>
    </div>

    <div class="section-block">
      <div class="callout-block callout-success">
        <div class="icon-holder">
          <i class="fas fa-clock"></i>
        </div>
        <div class="content">
          <h4 class="callout-title">Useful Tip:</h4>
          <p>
            You can use this online
            <a
              href="https://www.timeanddate.com/worldclock/converter.html"
              target="_blank"
              >Time Zone Converter</a
            >
            to easily convert time between different time zones.
          </p>
        </div>
      </div>

      <div class="code-block">
        <ol>
          <li>
            <h6>Detecting Browser’s Timezone:</h6>
            <p>
              You can detect the browser's timezone using the
              <br />
              <b>Intl.DateTimeFormat().resolvedOptions().timeZone</b>
              method:
            </p>
            <code-block :content="contentWithBrowserTimezone" />
          </li>
          <li>
            <h6>
              Handling Scenarios Where the Browser's Timezone is Unreliable:
            </h6>
            <p>
              In cases where the browser's timezone is unreliable or
              unavailable, fallback logic can be used to default to UTC or any
              other predefined timezone.
            </p>
            <code-block :content="contentWithoutBrowserTimezone" />
          </li>
          <li>
            <h6>Converting Server Timestamps to Browser's Timezone:</h6>
            <p>
              To convert server-side timestamps (which should always be in UTC)
              to the browser's timezone, you can use the Date object combined
              with the timezone detected earlier.
            </p>
            <code-block :content="convertServerTimestamps" />
          </li>
        </ol>
      </div>
    </div>
  </section>
</template>
<script>
import "../assets/css/styles.css";
import "../assets/plugins/simplelightbox/simple-lightbox.min.css";
import "../assets/plugins/elegant_font/css/style.css";
import "../assets/plugins/prism/prism.css";
import "../assets/plugins/bootstrap/css/bootstrap.min.css";
import CodeBlock from "./CodeBlock.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "BrowserTimezone",
  components: {
    CodeBlock
  },
  data() {
    return {
      contentWithBrowserTimezone: `  
    function getBrowserTimeZone() {
      return Intl.DateTimeFormat().resolvedOptions().timeZone;
    }
    console.log("Browser Timezone: ", getBrowserTimeZone());
        `,
      contentWithoutBrowserTimezone: `function getSafeBrowserTimeZone() {
    const timezone = Intl.DateTimeFormat().resolvedOptions().timeZone;
    return timezone ? timezone : 'UTC';  // Fallback to UTC if unavailable
}

console.log("Safe Timezone: ", getSafeBrowserTimeZone());`,
      convertServerTimestamps: `function convertToBrowserTimeZone(utcDate) {
    const browserTimeZone = getBrowserTimeZone();
    const date = new Date(utcDate);
    return date.toLocaleString("en-US", { timeZone: browserTimeZone });
}

// Example usage
const serverTimestamp = '2024-10-17T10:00:00Z'; // UTC timestamp from the server
console.log("Converted Timestamp: ", convertToBrowserTimeZone(serverTimestamp));`
    };
  },
  mounted() {},
  methods: {
    renderContent() {
      return;
    }
  }
};
</script>
<style scoped>
.timezone {
  background-color: #b1b5c7; /* Faint gray background */
  padding: 5px;
  border-radius: 5px;
}
</style>
