<template>
  <div>
    <div class="container">
      <div class="doc-body row">
        <div class="doc-content col-md-12 col-12 order-1">
          <div class="content-inner">
            <section id="code-section" class="doc-section">
              <div id="html" class="section-block">
                <VCodeBlock
                  :code="sanitizedHtmlContent"
                  highlightjs
                  lang="javascript"
                  copySuccessText="Copied!"
                />
              </div>
            </section>
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
import VCodeBlock from "@wdns/vue-code-block";
// import { defineProps, computed } from "vue";
// import DOMPurify from "dompurify";

export default {
  name: "CodeBlock",
  props: ["content"],
  components: {
    VCodeBlock
  },
  mounted() {},
  data() {
    return {
      copySuccess: false,
      successMessage: "Code copied to clipboard!",
      sanitizedHtmlContent: this.content
    };
  },
  methods: {
    copyToClipboard() {
      const codeText = this.$refs.codeBlock.innerText;
      navigator.clipboard
        .writeText(codeText)
        .then(() => {
          this.copySuccess = true;
          setTimeout(() => {
            this.copySuccess = false;
          }, 2000); // Hide success message after 2 seconds
        })
        .catch((err) => {
          console.error("Failed to copy: ", err);
        });
    }
  }
};
</script>

<style>
.code-block {
  position: relative; /* Positioning for the icon */
  padding: 10px;
  background-color: #f5f5f5; /* Light background for the code block */
  border-radius: 5px; /* Rounded corners */
  overflow: auto; /* Ensure overflow is handled */
}

.copy-icon {
  cursor: pointer; /* Change cursor to pointer */
  margin-left: 10px; /* Space between icon and text */
  font-size: 1.2em; /* Increase icon size */
  color: #007bff; /* Icon color */
  transition: color 0.3s; /* Smooth color transition */
}

.copy-icon:hover {
  color: #0056b3; /* Darker color on hover */
}
</style>
