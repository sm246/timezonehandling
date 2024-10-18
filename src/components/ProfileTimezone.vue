<template>
  <section id="profile-timezone-section" class="doc-section">
    <h2 class="section-title">Using Profile Timezone</h2>
    <div class="section-block">
      <div class="code-block">
        <ol>
          <li>
            <h6>Using User-Configured Timezone at Profile Levels:</h6>
            <p>
              If the user has configured a timezone in their profile settings,
              that timezone should take precedence over the browser’s detected
              timezone.
              <br />
              <b>Assume User Timezone from Profile:</b>
            </p>
            <code-block :content="contentWithUserConfigured" />
          </li>
          <li>
            <h6>Ensuring Timestamps Are Stored in UTC</h6>
            <p>
              All timestamps should be stored in UTC format in your database,
              and they can be converted to the user-configured timezone when
              needed.
              <br />
              <b>Example: Storing a Timestamp in UTC</b>
            </p>
            <code-block :content="contentWithTimeStampUTC" />
          </li>
          <li>
            <h6>Converting UTC to User-Configured Timezone:</h6>
            <code-block :content="convertUTCToUserConfigured" />
          </li>
          <li>
            <h6>Handling Real-Time Timezone Changes for Logged-In Users:</h6>
            <p>
              If a user changes their timezone in real-time (e.g., in profile
              settings), you should re-fetch their timezone and re-render the
              timestamps accordingly.
              <br />
              <b>Example of Handling Timezone Changes in Real-Time:</b>
            </p>
            <code-block :content="convertRealTimezone" />
          </li>
          <div>
            <h6>Additional Considerations:</h6>
            <ul style="list-style-type: square">
              <li>
                Use a library like moment-timezone if you need to handle complex
                timezone calculations or daylight saving time (DST).
              </li>
              <li>
                Ensure the server always sends timestamps in UTC to avoid
                timezone-related bugs.
              </li>
            </ul>
            <p>
              <br />
              <b>Example Using moment-timezone for Timezone Conversion:</b>
            </p>
            <h6 id="moment-timezone">Installation</h6>
            <p>You can install moment-timezone via npm .</p>
            <h6>Using npm</h6>
            <code-block :content="npmPackage" />
            <h6>Basic Usage</h6>
            <p>
              Here's a simple example to demonstrate how to use Moment Timezone:
            </p>
            <h6>Example: Converting Time Zones</h6>
            <code-block :content="basicUsage" />
            <h6>Formatting Dates</h6>
            <p>You can format dates in various ways. Here's an example:</p>
            <code-block :content="formattingDates" />
          </div>
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
      contentWithUserConfigured: ` // Simulate user profile data
const userProfile = {
  timezone: 'America/New_York'  // Example of a user-configured timezone
};

function getUserTimeZone() {
    return userProfile.timezone || getBrowserTimeZone();  // Fallback to browser timezone
}

console.log("User Timezone: ", getUserTimeZone());`,
      contentWithTimeStampUTC: `function getCurrentUTCTimestamp() {
    return new Date().toISOString();  // Generates the current timestamp in UTC
}

console.log("UTC Timestamp: ", getCurrentUTCTimestamp());`,
      convertUTCToUserConfigured: `function convertToUserTimeZone(utcDate) {
    const userTimeZone = getUserTimeZone();
    const date = new Date(utcDate);
    return date.toLocaleString("en-US", { timeZone: userTimeZone });
}

// Example usage
const utcTimestamp = '2024-10-17T10:00:00Z';  // Example UTC timestamp from server
console.log("User Timezone Timestamp: ", convertToUserTimeZone(utcTimestamp));`,
      convertRealTimezone: `// Simulate a real-time update to user profile
function updateUserTimeZone(newTimeZone) {
    userProfile.timezone = newTimeZone;  // Update user profile with the new timezone
    console.log("Updated User Timezone: ", getUserTimeZone());
    // Rerender or refresh timestamps
}

// Example of real-time change
updateUserTimeZone('Europe/London');

// After the change
console.log("Converted Time: ", convertToUserTimeZone(serverTimestamp));`,
      npmPackage: `npm install moment moment-timezone`,
      basicUsage: `// Import moment and moment-timezone
const moment = require('moment-timezone');

// Get the current time in UTC
let nowUtc = moment.utc();
console.log("Current time in UTC:", nowUtc.format());

// Convert to New York time
let newYorkTime = nowUtc.tz('America/New_York');
console.log("Current time in New York:", newYorkTime.format());

// Convert to Tokyo time
let tokyoTime = nowUtc.tz('Asia/Tokyo');
console.log("Current time in Tokyo:", tokyoTime.format());
`,
      formattingDates: `let now = moment();
let formattedDate = now.tz('Europe/London').format('YYYY-MM-DD HH:mm:ss');
console.log("Current time in London:", formattedDate);
`
    };
  },
  mounted() {}
};
</script>
<style scoped>
.timezone {
  background-color: #b1b5c7; /* Faint gray background */
  padding: 5px;
  border-radius: 5px;
}
</style>
