<script setup>
    import { ref, computed } from 'vue';
    import BlogPost from "./components/BlogPost.vue";
    const blogs = ref([
        {id:1,
        title:"vue3 基础教程",
        content:"vue3在vue2的基础上发生了重大的变化",
        link:"/vue3-turtorial"},
        {id:2,
        title:"react18 基础教程",
        content:"react18在react17的基础上发生了重大的变化",
        link:"/react18-turtorial"},
        {id:3,
        title:"javascript 基础教程",
        content:"javascript和node是什么关系，这是一个很好的问题",
        link:"/javascript-turtorial"},

    ]);
	const total = computed(() => blogs.value.length);
    const showTotal = ref(true);
    function toggleTotal() {
        showTotal.vaule = !showTotal.value;
    }
    const initialBlogForm = {
        title:"",
        content:"",
        link:"",
    };
    const blogFrom = ref({ ... initialBlogForm })
    function addPost() {
        blogs.value.push(
            {
                id:blogs.value.length + 1,
                ... blogFrom.value,
            }
        )
        blogFrom.value = { ... initialBlogForm }
    }
    function handleTitleClick(title) {
        console.log(title);
        
    }
</script>

<template>
    <BlogPost @titleClick="handleTitleClick" v-for="blog in blogs" :key="blog.id" :title="blog.title" :content="blog.content" :link="blog.link">
        <button>分享到微信</button>
    </BlogPost>
	<!--
    <h3 v-if="showTotal">总共 {{blogs.length}} 篇</h3>
	-->
    <h3 v-if="showTotal">总共 {{total}} 篇</h3>
    <button @click="toggleTotal">{{showTotal ? "隐藏" : "显示"}}总数</button>
    <form @submit.prevent="addPost">
        <label for="blogTitle">博客标题</label>
        <input type="text" id="blogTitle" v-model="blogFrom.title"/>
        <label for="content">内容</label>
        <textarea id="content" cols="30" rows="10" v-model="blogFrom.content"></textarea>
        <label for="link">链接</label>
        <input type="text" id="link" v-model="blogFrom.link" />
        <button type="submit">提交</button>
    </form>
</template>
<style scoped>
form {
    display: grid;
    margin-top:2em;
}
</style>
