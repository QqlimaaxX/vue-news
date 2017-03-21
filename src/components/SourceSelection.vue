<template>
	<div>
		<div class="jumbotron">
			<h2><span class="glyphicon glyphicon-list-alt"></span> News List</h2>
			<h4>Select News Source</h4>
			<select class="form-control" v-on:change="sourceChanged">
				<option v-for="source in sources" :value="source.id">{{source.name}}</option>
			</select>

			<div v-if="source" style="padding-top:10px">
				<a :href="source.url" class="btn btn-primary" target="_blank">Visit {{source.name}}</a>
				<h6>{{source.description}}</h6>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		name: 'source-selection',
		data(){
			return{sources:[],
			source:"",
			}
		},
		created:function(){
			this.$http.get('https://newsapi.org/v1/sources/?language=en')
			.then(response => {
				this.sources = response.data.sources;
			})
		},
		methods:{
			sourceChanged:function(e){
				for(var i=0;i<this.sources.length;i++){
					if(this.sources[i].id===e.target.value){
						this.source = this.sources[i];
						return;
					}
				}
			}
		}
	}
</script>

<style scoped>

</style>