<template id="post-list">
	<div class="row">
		<div class="pull-right">
			<router-link class="btn btn-xs btn-primary" v-bind:to="{path: '/add-post'}">
				<span class="glyphicon-plus"></span>
				Add new Post
			</router-link>
			<br><br>
		</div>

		<table class="table table-bordered">
			<thead>
				<tr>
					<th>#</th>
					<th>Post Title</th>
					<th>Post Body</th>
					<th class="col-md-2">Action</th>
				</tr>
			</thead>

			<tbody>
				<tr v-for="(post, index) in filteredPosts">
					<td>{{ index + 1 }}</td>
					<td>{{ post.title }}</td>
					<td>{{ post.body }}</td>
					<td>
						<router-link class="btn btn-info btn-xs" v-bind:to="{name: 'Viewpost', params: {id: post.id}}">Show</router-link>
						<router-link class="btn btn-warning btn-xs" v-bind:to="{name: 'Editpost', params: {id: post.id}}">Edit</router-link>
						<router-link class="btn btn-danger btn-xs" v-bind:to="{name: 'Deletepost', params: {id: post.id}}">Delete</router-link>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
	export default {
		data: function() {
			return {
				posts: ''
			};
		},
		created: function() {
			let url = 'http://localhost:8000/posts';
			Axios.get(url).then((response) => {
				this.posts = response.data;
			});
		},
		computed: {
			filteredPosts: function(){
				if(this.posts.length) {
					return this.posts;
				}
			}
		}
	}
</script>