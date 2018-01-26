<template>
  <div class="newslist">
    <ul class="media">
      <li class="media__item" v-for="article in articles">
        <div class="media__thumb">
          <a class="media__thumb-link" :href="article.url" target="_blank">
            <div class="media__thumb-img"
              :style="{ backgroundImage: 'url(' + article.urlToImage + ')' }"></div>
            <!-- <img class="media__thumb-img" :src="article.urlToImage"> -->
          </a>
        </div>
        <div class="media__preview">
          <a class="media__preview-link" :href="article.url" target="_blank">
            <h4 class="media__preview-title">
                {{ article.title }}
            </h4>
          </a>
          <h5 class="media__preview-author" v-if="article.author"><i>by {{ article.author }}</i></h5>
          <p class="media__preview-body">{{ article.description }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'newslist',
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    updateSource: function (source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=8961957442974a6bbe445d340409c39c')
        .then(response => {
          this.articles = response.data.articles
        })
    }
  },
  created: function () {
    this.updatedSource(this.source)
  },
  watch: {
    source: function (val) {
      this.updateSource(val)
    }
  }
}
</script>

<style lang="scss" scoped>
.newslist {
  max-width: 1440px;
  margin: 0 auto;
  margin-bottom: 50px;
  padding: 0 10px;
}
.media {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
  grid-gap: 20px;
  list-style-type: none;
  margin: 0;
  padding: 0;

  &__item {
    display: flex;
    background: white;
    box-shadow: 0 2px 3px rgba(black, .1);
    border-radius: 4px;
  }
  &__thumb {
    position: relative;
    display: flex;
    flex: 1 0 auto;
    width: 50%;
    border-radius: 4px 0 0 4px;
    background: #000;
    overflow: hidden;
  }
  &__thumb-link {
    // width: 100%;
  }
  &__thumb-img {
    position: absolute;
    display: block;
    width: 100%;
    height: 100%;
    background-position: center center;
    background-size: cover;
  }
  &__preview {
    width: 50%;
    padding: 15px;
  }
  &__preview-link {
    text-decoration: none;
  }
  &__preview-title {
    margin: 0;
    font-size: 20px;
    line-height: 1.3;
  }
  &__preview-author {
    margin: 10px 0 0;
  }
  &__preview-body {

  }
}
</style>
