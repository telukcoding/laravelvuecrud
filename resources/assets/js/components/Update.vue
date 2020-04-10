<template>
    <div class="container"> 
                <div class="card card-default">
                    <div class="card-header" style="text-align:center">Edit Post</div>

                    <div class="card-body">
                      <form v-on:submit="submitPostEdit()">
                          <div class="form-group">
                              <input type="text" v-model="posts.title" class="form-control">
                          </div>
                            <div class="form-group">
                              <textarea rows="5" type="text" v-model="posts.description" class="form-control"></textarea>
                          </div>
                            <div class="form-group">
                              <router-link to="/" class="btn btn-warning">Cancel</router-link>
                             <button class="btn btn-success">Update</button>
                          </div>
                      </form>
                    </div>
                </div> 
    </div>
</template>

<script> 

export default {
  data:function() {
    return {
      posts: {
        title:'',
        description:'',
      },
      errors: []
    }
  },
  created() {
    let id = this.$route.params.id; 
    axios.get('/posts/' + id + '/edit')
    .then(response => { 
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    }) 
  }, 
 methods:{
  submitPostEdit() {
    let id = this.$route.params.id; 
    axios.patch('/posts/' + id, this.posts)
    .then(response => {
      console.log(response)
      this.$router.push({path:'/'})
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
 
   }
  }
}
</script>