<template>
  <div class="posts-page">
    <PostList :posts="loadedPosts" />
  </div>
</template>

<script>
import PostList from "@/components/Posts/PostList";

export default {
  components: {
    PostList
  },
  fetch(context){
    if(context.store.state.loadedPosts.length  > 0 ) {
      return null
    }
  return new Promise((resolve,reject) => {
    setTimeout(() => {
      resolve({
        loadedPosts : [
          {
            id : '1' ,
            title : 'First Post ' ,
            previewText : 'first Post Text',
            thumbnail : 'https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg'
          },
          {
            id : '2' ,
            title : 'Second Post ' ,
            previewText : 'Second Post Text',
            thumbnail : 'https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg'
          },
          {
            id : '3' ,
            title : 'Third Post ' ,
            previewText : 'Third Post Text',
            thumbnail : 'https://static.pexels.com/photos/270348/pexels-photo-270348.jpeg'
          },
        ]
      })
    },2000)
  })
    .then(data => {
      context.store.commit('setPosts',data.loadedPosts)
    })
    .catch(e =>  {
      context.error(e)
    })
  },
  computed : {
    loadedPosts() {
      return this.$store.getters.loadedPosts
    }
  }
};
</script>


<style scoped>
.posts-page {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
