<template>
  <section id="profile-timezone-section" class="doc-section">
    <h2 class="section-title">Using Database Timezone</h2>
    <div class="section-block">
      <div class="code-block">
        <ol>
          <li>
            <h6>Storing Timestamps in UTC :</h6>
            <p>
              Storing timestamps in UTC (Coordinated Universal Time) is widely
              regarded as a best practice in database design. This approach
              simplifies the handling of time-related data, especially when
              dealing with users across different time zones. Here are some key
              points to consider:
            </p>
            <ul>
              <li>
                <b>Simplicity in Comparisons: </b>Storing all timestamps in UTC
                ensures that you have a consistent reference point, making it
                easier to perform comparisons and calculations without worrying
                about local time variations.
              </li>
              <li>
                <b>Consistency: </b>When timestamps are stored in UTC, you can
                easily compare them without needing to account for time zone
                differences.
              </li>
              <li>
                <b>Avoiding Daylight Saving Time Issues:</b> UTC does not change
                with daylight saving time, which can complicate time
                calculations if local times are used.
              </li>
            </ul>
          </li>
          <li>
            <h6>
              Handling Timezones in Database to Aggregate Results in User’s
              Timezone
            </h6>
            <ol>
              <li>
                <h6>PostgreSQL:</h6>
                <p>
                  In PostgreSQL, timestamps are often stored in UTC to ensure
                  consistency across timezones. When retrieving data, you can
                  use the AT TIME ZONE construct to convert UTC to the user's
                  local timezone.
                </p>
                <h6>
                  Query Example (PostgreSQL) to Group by Day in User's Timezone:
                </h6>
                <code-block :content="postgresql" />
                <h6>Best Practices for Indexing (PostgreSQL):</h6>
                <ul>
                  <li>Store timestamps in TIMESTAMP WITH TIME ZONE.</li>
                  <li>
                    Use indexes on the UTC-based timestamp to improve
                    performance, as PostgreSQL converts them efficiently during
                    queries.
                  </li>
                </ul>
              </li>
              <li>
                <h6>MySQL:</h6>
                <p>
                  Similar to PostgreSQL, MySQL stores timestamps in UTC, and
                  conversion can be done using the CONVERT_TZ function.
                </p>
                <h6>
                  Query Example (MySQL) to Group by Month in User's Timezone:
                </h6>
                <code-block :content="mysql" />
                <h6>Best Practices for Indexing (MySQL):</h6>
                <ul>
                  <li>Use TIMESTAMP datatype to store UTC time.</li>
                  <li>
                    Ensure the indexed field is the UTC timestamp, then apply
                    timezone conversions only during the retrieval.
                  </li>
                </ul>
              </li>
              <li>
                <h6>MongoDB:</h6>
                <p>
                  MongoDB stores dates in ISODate format (UTC by default). You
                  can aggregate data and convert to the user's timezone using
                  $dateToString.
                </p>
                <h6>
                  Query Example (MongoDB) to Group by Week in User's Timezone:
                </h6>
                <code-block :content="mongodb" />
                <h6>Best Practices for Indexing (MongoDB):</h6>
                <ul>
                  <li>Use an index on the UTC-based timestamp field.</li>
                  <li>
                    Perform timezone conversion only at the aggregation level to
                    optimize query performance.
                  </li>
                </ul>
              </li>
            </ol>
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
      postgresql: `SELECT 
  date_trunc('day', timestamp_column AT TIME ZONE 'UTC' AT TIME ZONE 'America/New_York') AS day,
  COUNT(*) AS event_count
FROM your_table
WHERE timestamp_column BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY day
ORDER BY day;`,
      mysql: `SELECT 
  DATE_FORMAT(CONVERT_TZ(timestamp_column, '+00:00', 'America/New_York'), '%Y-%m') AS month,
  COUNT(*) AS event_count
FROM your_table
WHERE timestamp_column BETWEEN '2024-01-01' AND '2024-12-31'
GROUP BY month
ORDER BY month;`,
      mongodb: `db.yourCollection.aggregate([
  {
    $project: {
      week: {
        $dateToString: { format: "%Y-%U", date: "$timestamp", timezone: "America/New_York" }
      }
    }
  },
  {
    $group: {
      _id: "$week",
      count: { $sum: 1 }
    }
  },
  { $sort: { _id: 1 } }
]);`
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
