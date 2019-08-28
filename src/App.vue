<template>
  <div class="container">
    <app-header :quoteCount="quotes.length" :maxQuotes="maxQuotes"></app-header>
    <app-new-quote @quoteAdded="newQuote"></app-new-quote>
    <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quote-grid>
    <div class="row">
      <app-alert :message="message" />
    </div>
  </div>
</template>

<script>
import QuoteGrid from "./components/QuoteGrid.vue";
import NewQuote from "./components/NewQuote.vue";
import Header from "./components/Header.vue";
import Alert from "./components/Alert.vue";

export default {
  data: function() {
    return {
      quotes: ["Just a Quote to see something"],
      maxQuotes: 10,
      message: "222"
    };
  },
  methods: {
    newQuote(quote) {
      if (this.quotes.length >= this.maxQuotes) {
        return alert("Please delete Quotes first!");
      }
      this.quotes.push(quote);
      const thumbs = quote.substr(0, quote.length > 10 ? 10 : quote.length);
      this.message = `New message ${thumbs}... added`;
    },
    deleteQuote(index) {
      this.quotes.splice(index, 1);
    }
  },
  created() {
    setTimeout(
      () => (this.message = "Info: Click on a Quote to delete it!"),
      100
    );
  },
  components: {
    appQuoteGrid: QuoteGrid,
    appNewQuote: NewQuote,
    appHeader: Header,
    appAlert: Alert
  }
};
</script>

<style>
</style>
