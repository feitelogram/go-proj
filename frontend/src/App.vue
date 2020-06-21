<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3 py-5">
        <h1>Welcome to Take A Peek!</h1>
        <br />
        <h5>
          Enter a URL below to see a screenshot of whatever website you'd like!
        </h5>
        <br />
        <form v-on:submit.prevent="makeWebsiteThumbnail">
          <div class="form-group">
            <input
              v-model="websiteUrl"
              type="text"
              id="website-input"
              placeholder="Enter a site to take a peek at!"
              class="form-control"
            />
          </div>
          <div class="form-group">
            <button class="btn btn-primary">Generate!</button>
          </div>
        </form>
        <img :src="thumbnailUrl" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',

  data() {
    return {
      websiteUrl: '',
      thumbnailUrl: '',
    };
  },

  methods: {
    makeWebsiteThumbnail() {
      axios
        .post('http://take-a-peek.herokuapp.com/api/thumbnail', {
          url: this.websiteUrl,
          headers: { 'Access-Control-Allow-Origin': '*' },
        })
        .then((response) => {
          this.thumbnailUrl = response.data.screenshot;
        })
        .catch((error) => {
          window.alert(`The API returned an error: ${error}`);
        });
    },
  },
};
</script>
