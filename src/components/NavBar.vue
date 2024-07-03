<template>
    <nav
        :class="['navbar', 'navbar-expand-lg', `navbar-${theme}`, `bg-${theme}`]"
    >
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li v-for="(page, index) in getPublishedPages" class="nav-item" :key="index">
                    <NavBarLink
                        :page="page"
                        :isActive="activePage === index"
                        @click.prevent="navLinkClick(index)"
                    />
                </li>
            </ul>
            <form class="d-flex">
                <button
                    class="btn btn-outline-success"
                    @click.prevent="changeTheme()"
                    >Toggle</button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavBarLink from './NavBarLink.vue';

export default {
    components  : {
        NavBarLink
    },
    props : ['pages', 'activePage', 'navLinkClick'],
    created () {
        this.getThemeSetting()
    },
    computed : {
        getPublishedPages() {
            return this.pages.filter(page => page.published);
        }
    },
    data() {
        return {
            theme : 'light'
        }
    },
    methods : {
        changeTheme() {
            let theme = 'light';
                if (this.theme == 'light') {
                    theme = 'dark';
                }

            this.theme = theme;
            this.storeThemeSetting()
            
        },
        storeThemeSetting() {
            localStorage.setItem("theme", this.theme)
        },
        getThemeSetting() {
            let theme = localStorage.getItem("theme")
                if (theme) {
                    this.theme = theme;
                }
        }
    },
}
</script>