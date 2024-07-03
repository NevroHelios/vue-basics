<template>
    <NavBar
        :pages="pages"
        :activePage="activePage"
        :nav-link-click="(index) => activePage = index"
    />
    <!-- <PageViewer
        v-if="pages.length > 0"
        :page="pages[activePage]"
    /> -->
    <Createpage
        :pageCreated = "pageCreated"
        />
</template>

<script>
import NavBar from './components/NavBar.vue'
import PageViewer from './components/PageViewer.vue'
import Createpage from './components/CreatePage.vue'

export default {
    components : {
        NavBar,
        PageViewer,
        Createpage
    },
    created() {
        this.getPages()
    },
    data() {
        return {
            activePage : 0,
            pages : []
        }
    },
    methods : {
        async getPages() {
            let res = await fetch('pages.json');
            let data = await res.json()

            this.pages = data;
        },
        pageCreated(pageObj){
            this.pages.push(pageObj)
        }
    }
}
</script>