<template>
	<div class="newslist">
		<div class="container">
			<ul class="media-list">
				<li class="media" v-for="article in articles">
					<div class="media-left">
						<a :href="article.url" target="_blank">
							<img class="media-object" :src="article.urlToImage">
						</a>
					</div>
					<div class="media-body">
						<h4 class="media-heading">
							<a :href="article.url" target="_blank">{{article.title}}</a>
						</h4>
						<h5><i>{{article.author}}</i></h5>
						<p>{{article.description}}</p>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	export default{
		name: 'news-list',
		props:['source'],
		data(){
			return{
				apikey:"b9c65a8b75424a56afe6f912b813a06a",
				articles:[]
			}
		},
		methods:{
			updateSource:function(source){
				this.$http.get('https://newsapi.org/v1/articles?source='+source+'&apiKey='+this.apikey)
					.then(response=>{
						this.articles = response.data.articles;
					})
			}
		},
		watch:{
			source:function(val){
				this.updateSource(val);
			}
		},
		created:function(){
			if(this.source){
				this.updateSource(this.source);
			}
				
		}
	}
</script>

<style scoped>

</style>