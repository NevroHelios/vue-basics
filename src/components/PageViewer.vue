<template>
    <div class="container">
        <!-- <p>{{ page }}</p> -->
        <h1>{{ page.pageTitle }}</h1>
        <p>{{ page.content }}</p>
    </div>
</template>

<script>
export default {
    props : ["page"]
}
</script>