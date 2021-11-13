<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
    <div id="graphdiv" v-html="graphHtml"></div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

import mermaid from "mermaid";
export default Vue.extend({
  name: "Home",
  components: {
    // HelloWorld,
  },
  data() {
    return {
      graphHtml: "",
    };
  },
  created() {
    this.graphHtml = mermaid.mermaidAPI.render(
      "erd",

      `erDiagram
Customer {
  id int
  name string
}
Item {
  id int
  name string
  price float
  customerId int
}
Item ||--|{ Customer : "[Customer.id] - [Item.customerId]"
`,
      (html: string) => {
        this.graphHtml = html;
        this.$nextTick(() => {
          document.getElementById("Item")?.addEventListener("click", () => {
            this.$buefy.dialog.alert({
              message:
                "Item clicked. There would be normalization options here",
            });
          });
          document.getElementById("Customer")?.addEventListener("click", () => {
            console.log("Customer clicked");
            this.$buefy.dialog.alert({
              message:
                "Customer clicked. There would be normalization options here",
            });
            console.log(document.getElementById("Item"));
          });
          var texts = document.getElementsByTagName('text')
          for (var i = 0; i < texts.length; i++) {
            if (texts[i].textContent == '[Customer.id] - [Item.customerId]') {
              texts[i].addEventListener('click', () => {
                this.$buefy.dialog.alert({
                  message:
                    "Relation clicked. There would be merging options here",
                });
              });
              break;
            }
          }
        });
      }
    );
  },
});
</script>
