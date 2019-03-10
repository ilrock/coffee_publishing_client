<template>
  <v-container grid-list-xs>
    <v-layout row wrap d-flex>
      <v-flex xs12 md6>
        <v-text-field v-model="post.title" label="Title" />
      </v-flex>
      <v-flex xs12 md-1 offset-md5 style="display: flex">
        <v-spacer></v-spacer>
        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn color="grey lighten-3" v-on="on" @click="showPreview = true">
              <v-icon class="pr-2">remove_red_eye</v-icon>
              Preview
            </v-btn>
          </template>
          <span>Preview</span>
        </v-tooltip>
      </v-flex>
    </v-layout>
    <no-ssr placeholder="Loading Your Editor...">
      <vue-editor placeholder="Write Something..." v-model="post.content">
      </vue-editor>
    </no-ssr>
    <v-layout row wrap>
      <v-flex xs12>
        <v-btn color="success" @click="onSaveAdnPublish">Save and publish</v-btn>
        <v-btn color="info">Save as a draft</v-btn>
      </v-flex>
    </v-layout>
    <v-layout v-for ="(blog, index) in posts" :key="index" row wrap>
      <v-flex xs12 class="title">
        {{ blog.title }}
      </v-flex>
      <v-flex xs12 v-html="blog.content"/>
    </v-layout>
    <full-page-modal 
      :content="post.content"
      :showModal="showPreview"
      @close="showPreview = false"/>
  </v-container>
</template>

<script>
import FullPageModal from '../components/FullPageModal'

export default {
  components: {
    FullPageModal
  },
  data () {
    return {
      showPreview: false,
      post: {
        title: '',
        content: ''
      }
    }
  },
  async asyncData ({ $axios }) {
    const { data } = await $axios.get('http://localhost:8000/api/v1/posts')
    console.log('Data', data)
    return {
      posts: data
    }
  },
  methods: {
    onSaveAdnPublish () {
      this.$axios.post('http://localhost:8000/api/v1/posts', this.post, {
        headers: {
          'x-auth-token': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ.sATpJ4lWyxl6jILnVTkTguWeV3GvqHYbz-p_rMssjOs'
        }
      })
        .then((res) => console.log(res))
    }
  }
}
</script>
