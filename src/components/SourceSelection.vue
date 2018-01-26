<template>
  <div class="sourceselection">
    <div class="source">
      <h2 class="source__title">News List</h2>
      <h4 class="source__instruction">Select a News Source</h4>
      <select class="source__control form__select" @change="sourceChanged">
        <option value="">Please select news source</option>
        <option v-for="source in sources" :value="source.id">
          {{ source.name }}
        </option>
      </select>

      <div v-if="source">
        <h6 class="source__description" >{{ source.description }}</h6>
        <a class="button button--primary" :href="source.url" target="_blank">
          More articles at {{ source.name }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'sourceselection',
  data () {
    return {
      sources: [],
      source: ''
    }
  },
  methods: {
    sourceChanged: function (e) {
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id === e.target.value) {
          this.source = this.sources[i]
        }
      }
      this.$emit('sourceChanged', e.target.value)
    }
  },
  created: function () {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources
      })
  }
}
</script>

<style lang="scss" scoped>
.source {
  padding: 50px 0;
  text-align: center;
  margin-bottom: 50px;
  background: #000;
  color: white;

  &__title {
    margin: 0;
  }
  &__instruction {
    margin: 10px 0;
  }
  &__description {
    font-size: 16px;
    font-weight: normal;
    max-width: 650px;
    margin: 25px auto 25px auto;
  }
}
</style>
