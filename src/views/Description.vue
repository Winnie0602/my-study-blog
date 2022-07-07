<template>
<Nav />
<div v-if="!error">
  <div class="whiteBG">
    <div class="post-head">
      <h2>{{post.title}}</h2>
      <div>
        <span v-for="tag in post.tags" :key="tag" class="tagsContainer">
          <router-link :to="{name: 'Tags', params:{tag} }" class="tag">
              # {{ tag }}
          </router-link>
        </span> 
      </div>
    </div>
    <div class="body">
      <p>{{post.body}}</p>  
      
    </div>
    
    
  </div>
</div>
<div v-else>
    {{error}}
</div>
</template>

<script>
import Nav from '../components/Nav.vue'
import getPost from '../composables/getPost'
import { useRoute } from 'vue-router'

export default {
    components:{ Nav },
    setup(){
      const route = useRoute()
      const { post, error, load } = getPost(route.params.id)

      load()
        
      return { post, error, load }
    }

}
</script>

<style scoped>
.tag{
    text-decoration: none;
    color: white;
    background-color: #275660;
    padding: 0.4rem;
    border-radius: 1rem;
    margin: 0 5px;

}
.whiteBG{
  background-color: #fff;
  border-radius: 2rem;
  height: 70vh;
  margin: 20px auto;
  padding: 20px;
}
h2{
  margin: 1rem 0rem;
}
P{
  line-height: 2rem;
}
.post-head{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media screen and (max-width: 1310px) {
    h2{
    margin: 0.5rem 0rem;
    font-size: 20px;
  }
    .post-head{
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
  }
  p{
    margin-top: 20px;
  }
  .tagsContainer{
    max-width: 100px;
    display: flex;
  }
  .tag{
      background-color: white;
      margin: 0px;
      color:#275660;
      border-bottom: 1px solid #275660;
      border-radius: 0px;
      padding: 0;
  }
}

</style>
