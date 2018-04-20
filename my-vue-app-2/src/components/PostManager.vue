<template>
  <div class="container-fluid mt-4">
    <h1 class="h1">{{post.title}}</h1>
    <h2>{{$route.query.thing}}</h2>
    <b-alert :show="loading" variant="info">Loading...</b-alert>
    <b-row>
      <b-col>
        <p class='lead'><strong>Title:</strong> {{post.title}}</p>
        <p>{{post.body}}</p>
      </b-col>
     
    </b-row>
  </div>
</template>

<script>
import api from '@/api'
export default {
  data () {
    return {
      loading: false,
      post: [],
      model: {}
    }
  },
  async created () {
    this.getPost(this.$route.params.id)
  },
  methods: {
    async populatePostToEdit (post) {
      this.model = Object.assign({}, post)
    },
    async getPost(id) {
      this.loading = true
      this.post = await api.getPost(id)
      this.loading = false
    },
  }
}
</script>