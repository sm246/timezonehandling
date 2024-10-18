<template>
  <section id="background-timezone-section" class="doc-section">
    <h2 class="section-title">
      Handling Timezones for Background Processes (e.g., Cron Jobs)
    </h2>
    <div class="section-block">
      <div class="code-block">
        <ol>
          <li>
            <h6>Consistent Timezone Management in Node.js Cron Jobs:</h6>
            <p>
              Use libraries like cron with explicit timezone configuration to
              handle scheduled tasks in Node.js.
            </p>
            <h6>Installation</h6>
            <p>You can install cron via npm .</p>
            <h6>Using npm</h6>
            <code-block :content="npmPackage" />
            <code-block :content="cron" />
          </li>
          <li>
            <h6>Handling Daylight Saving Time (DST) in Scheduled Tasks:</h6>
            <ul>
              <li>
                Use timezone-aware libraries like moment-timezone to ensure that
                tasks adjust correctly during DST transitions.
              </li>
              <li>
                Schedule tasks in UTC if possible, then perform timezone
                conversions at the task level.
              </li>
            </ul>
            <h6>Installation</h6>
            <p>
              You can install
              <a href="#moment-timezone">moment-timezone</a> via npm .
            </p>
            <br />
            <h6>Example Using moment-timezone to Handle DST:</h6>
            <code-block :content="dayLightCron" />
          </li>
          <li>
            <h6>Strategies for Ensuring Consistent Timezone Management:</h6>
            <ul>
              <li>
                <h6>Avoid scheduling tasks in local time:</h6>
                Always store and schedule tasks in UTC to ensure consistency
                across deployments.
              </li>
              <li>
                <h6>Check DST adjustments:</h6>
                Regularly test your tasks during DST transitions to ensure the
                schedule remains correct.
              </li>
              <li>
                <h6>Use Timezone-Aware Databases:</h6>
                Store timestamps in UTC and only apply timezone transformations
                when retrieving or displaying data.
              </li>
              <li>
                <h6>Best Practices Summary:</h6>
                Database: Store timestamps in UTC and convert to the user’s
                timezone during retrieval. Index on the UTC field to optimize
                performance.
              </li>
              <li>
                <h6>Background Processes:</h6>
                Schedule tasks in UTC and handle timezone conversion at the task
                level using libraries like cron, node-schedule.
              </li>
              <li>
                <h6>Daylight Saving Time (DST):</h6>
                Use timezone-aware libraries to ensure that tasks adapt to DST
                changes automatically.
              </li>
            </ul>
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
      cron: `const cron = require('node-cron');
const moment = require('moment-timezone');

cron.schedule('0 0 * * *', () => {
  // Task runs at midnight in the user's timezone
  const currentTime = moment().tz('America/New_York').format();
  console.log('Running task at:', currentTime);
}, {
  timezone: 'America/New_York'
});`,
      npmPackage: `npm install cron`,
      dayLightCron: `const moment = require('moment-timezone');

// User's timezone
const userTimezone = 'Europe/London';

// Task time in UTC
const utcDate = moment.utc(); // Current time in UTC

// Convert UTC time to user's timezone, handling DST
const userTime = utcDate.tz(userTimezone).format('YYYY-MM-DD HH:mm:ss Z');

console.log('Task running at user time:', userTime);
`
    };
  },
  mounted() {}
};
</script>
<style scoped>
.timezone {
  background-color: #b1b5c7;
  padding: 5px;
  border-radius: 5px;
}
</style>
