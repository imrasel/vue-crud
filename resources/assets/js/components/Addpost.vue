<template id="add-post">
	<div class="container">
		<h3>Add New Post</h3>

		<form v-on:submit.prevent = "createPost">
			<div class="form-group">
				<label for="">Title</label>
				<input id="add-title" v-model="post.title" required type="text" class="form-control">
			</div>

			<div class="form-group">
				<label for="">Body</label>
				<textarea class="form-control" v-model="post.body" rows="10"></textarea>
			</div>
			
			<button type="submit" class="btn btn-xs btn-primary">Create Post</button>
			<router-link class="btn btn-xs btn-warning" v-bind:to="'/'">Cancel</router-link>
		</form>
	</div>
</template>

<script>
	export default {
		data: function() {
			return {
				post: {
					title: '',
					body: '',
				}
			};
		},
		methods: {
			createPost: function(){
				let url = 'http://localhost:8000/posts';
				Axios.post(url, this.post).then((response) => {
					this.$router.push({
						name: 'Listposts'
					})
				})
			}
		}
	}
</script>