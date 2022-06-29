<template>
    <section>
        <h1> Posts</h1>
        <div v-if="posts.length > 0" class="row justify-content-center" style="gap: 15px;">
            <div class="card" style="width: 18rem;" v-for="(post) in posts" :key="post.id">
                <div class="card-body">
                    <h5 class="card-title">{{post.title}}</h5>
                    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                    <router-link :to="{ name: 'single-post', params: { slug: post.slug } }"  class="btn btn-primary">Visualizza Post</router-link>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    name: 'PostsComponent',
    data(){
        return {
            posts: []
        }
    },
    created(){
        axios.get('/api/posts').then((response)=>{
            this.posts = response.data;
        }).catch((error)=>{
            console.log(error);
        })
    }
}
</script>
<style lang="scss">

</style>
