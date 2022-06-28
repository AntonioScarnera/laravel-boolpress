<template>
    <header>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="container-fluid">
                <!--<router-link :to="{name: menuItem[0].routeName}" class="navbar-brand">Boolpress</router-link>-->
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNav">
                    <div v-for="(item, index) in menuItem" :key="index">
                        <router-link :to="{name: item.routeName}" class="nav-link">{{item.label}}</router-link>
                    </div>
                </div>
            </div>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'HeaderComponent',
    data(){
        return{
            menuItem:[
                {
                    label: 'Home',
                    routeName: 'home'
                },
                {
                    label: 'Posts',
                    routeName: 'posts'
                },
                {
                    label: 'Chi Siamo',
                    routeName: 'about'
                },
                {
                    label: 'Contatti',
                    routeName: 'contact'
                }
            ]
        }
    }
}
</script>

<style lang="scss">
</style>
