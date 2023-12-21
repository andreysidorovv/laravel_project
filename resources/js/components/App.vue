<template>
    <ul class="container">
        <li v-for="a in this.articles" class="alert alert-primary" role="alert">
            Добавлена новая статья
            <strong>
                <a v-bind:href="'article/' + a.id">
                    {{ a.title }}
                </a>
            </strong>
        </li>
    </ul>
</template>
<script>
export default {
    data() {
        return {
            articles: [],
        };
    },
    created() {
        window.Echo.channel('my-channel').listen('EventNewArticle', (data) => {
            console.log(data);
            this.articles.push(data.article);
        })
    }
}
</script>
