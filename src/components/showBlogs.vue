<template>
    <div id="show-blogs">
        <h1>All Blog Articles</h1>
        <input type="text" v-model="search" placeholder="search blogs" class="searchBar" />
        <div v-for="blog in filteredBlogs" class="single-blog">
            <router-link v-bind:to ="'/blog/' + blog.id"><h2 v-rainbow>{{ blog.title | toUppercase }}</h2></router-link>
            <article>{{ blog.body }}</article>
        </div>
    </div>
</template>

<script>
import searchMixin from '../mixins/searchMixin';

export default {
    data () {
        return {
            blogs: [],
            search: ''
            // 검색할 값 
        }
    },
    methods: {

    },
    created() {
        this.$http.get('https://vuejs-practice-7bdb9-default-rtdb.firebaseio.com/posts.json').then(function(data){
            return data.json()
        }).then(function(data){
            var blogsArray = [];
            for(let key in data) {
                data[key].id = key
                blogsArray.push(data[key]);
            }
            this.blogs = blogsArray;
        });
    },
    computed: {
        // filteredBlogs: function(){
        //     return this.blogs.filter((blog) => {
        //         return blog.title.match(this.search);
        //     });
        // }
    },
    filters: {
        toUppercase(value){
            return value.toUpperCase();
            //locally
        }
    },
    directives: {
        'rainbow' :{
            bind(el, binding, vnode){
                el.style.color = "#" + Math.random().toString(16).slice(2, 8);
            }
        }
    },
    mixins: [searchMixin]
} 
// http -> 브라우저와 서버간 데이터를 주고 받는 통신 프로토콜
// http request = 데이터 request
// get -> 서버에서 데이터를 가져옴 서버 주소인 /api/data 로부터 값을 불러 올 때 사용
// axios 요청 시 파라메터 정보(/api/todos/1)를 같이 입력하여 정보를 얻어 올 수 있다.
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
.searchBar{
    width: 800px;
}
</style>