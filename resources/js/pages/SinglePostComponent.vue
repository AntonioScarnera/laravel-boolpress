<template>
    <section>
        <div v-if="post">
            <h1 >{{post.title}}</h1>
            <img :src="`/storage/${post.image}`" alt="">
            <p v-html="post.content"></p>
            <ul v-if="post.tags">
                <li v-for="tag in post.tags" :key="tag.id">{{tag.name}}</li>
            </ul>
            <div>
                <form @submit.prevent = "addComment()">
                    <div class="form-group">
                        <label for="username" class="form-label">Inserisci il nome</label>
                        <input class="form-control" type="text" name="username" v-model="formData.username">
                    </div>
                    <div class="form-group">
                        <label for="content" class="form-label">Inserisci il commento</label>
                        <textarea class="form-control" name="content" id="" cols="30" rows="10" v-model="formData.content"></textarea>
                    </div>
                        <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
            <div v-if="post.comments.length > 0">
                <h4>Commenti:</h4>
                <div v-for="comment in post.comments" :key="comment.id">
                    <br>
                    {{comment.username}}: <br>
                    {{comment.content}}
                </div>
            </div>
        </div>

    </section>
</template>
<script>
export default {
    name: 'SinglePostComponent',
    data(){
        return{
            post: null,
            formData: {
                username: '',
                content: '',
                post_id: ''
            }
        }
    },
    methods:{
        addComment(){
            axios.post("/api/comments", this.formData)
                .then((response)=>{
                    console.log(response);
                    this.post.comments.push(response.data);
                })
                .catch((error)=> {
                    console.log(error);
                });
        }
    },
    mounted(){
        const slug = this.$route.params.slug;
        axios.get(`/api/posts/${slug}`).then((response) => {
            this.post = response.data;
            this.formData.post_id = this.post.id;
            console.log(this.formData.post_id);
        }).catch((error) => {
            // handle error
            this.$router.push({name: 'page-404'});
        })
    }
}
</script>
<style lang="scss">
 img {
    width:200px;
 }

</style>
