<template>
    <div>

       <h1>Cypress Vue App Test</h1>
       <p> End to end testing of a vue.js application using Cypress.io </p>

       <div class="col-md-12 form-wrapper">
          <h2> Create Post </h2>
          <form id="create-post-form" @submit.prevent="createPost">
               <div class="form-group col-md-12">
                <label for="title"> Title </label>
                <input type="text" id="title" v-model="title" name="title" class="form-control" placeholder="Enter title">
               </div>
              <div class="form-group col-md-12">
                  <label for="description"> Description </label>
                  <input type="text" id="description" v-model="description" name="description" class="form-control" placeholder="Enter Description">
              </div>
              <div class="form-group col-md-12">
                  <label for="body"> Write Content </label>
                  <textarea id="body" cols="30" rows="5" v-model="body" class="form-control"></textarea>
              </div>
              <div class="form-group col-md-12">
                  <label for="author"> Author </label>
                  <input type="text" id="author" v-model="author" name="author" class="form-control">
              </div>

              <div class="form-group col-md-4 pull-right">
                  <button class="btn btn-success" type="submit"> Create Post </button>
              </div>          
          </form>
        </div>
    
        <div class="row">
           <div class="col-md-4" v-for="post in posts" :key="post.id">
              <div class="card mb-4 shadow-sm">
                <div class="card-body">
                   <h2 class="card-img-top">{{ post.title }}</h2>
                  <p class="card-text">{{ post.body }}</p>
                  <div class="d-flex justify-content-between align-items-center">
                    <div class="btn-group" style="margin-bottom: 20px;">
                       <button class="btn btn-sm btn-outline-secondary" v-on:click="deletePost(post.id)">Delete Post</button>
                    </div>
                  </div>

                  <div class="card-footer">
                    <small class="text-muted">by: {{ post.author}} </small>
                  </div>
                   
                </div>
              </div>
            </div>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      id: "",
      title: "",
      description: "",
      body: "",
      author: "Olususi Oluyemi",
      postData: ""
    };
  },
  created() {
    this.fetchPosts();
  },
  methods: {
    createPost() {
      this.postData = {
        id: this._timeInMilliseconds(),
        title: this.title,
        description: this.description,
        body: this.body,
        author: this.author
      };
      this.posts = [...this.posts, this.postData];
      this._clearForm();
    },

    fetchPosts() {
      return this.posts;
    },
    deletePost(id) {
      let index = this.posts.findIndex(post => post.id === id);
      if (index === -1) {
        console.log("Post not found");
      }
      this.posts.splice(index, 1);
    },

    _clearForm() {
      this.title = "";
      this.body = "";
      this.description = "";
    },

    _timeInMilliseconds() {
      const date = new Date();
      return date.getTime();
    }
  }
};
</script>

