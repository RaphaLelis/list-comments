<template>
	<div class="container" style="background-color: white;">
		<h1>Comentários</h1>
		<hr/>
		<FormToDo v-on:add-todo = "addComments"></FormToDo>
		<div class="list-group">
			<div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.id">
				<span class="comment_author">Autor: <strong>{{comment.name}}</strong></span>
				<p>{{comment.message}}</p>
				<div>
					<a href="#" title="Excluir" v-on:click.prevent="deleteComment(index)">Excluir</a>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import FormToDo from './FormToDo.vue'

export default {
	components:{
		FormToDo
	},
	data() {
		return {
			comments: []
		}
	},
	methods: {
		addComments(comment){
			this.comments.push(comment);
		},
		deleteComment(index) {
			this.comments.splice(index, 1);
		}
	},
	computed: {
		allComments() {
			return this.comments.map(comment => ({
				...comment,
				name: comment.name.trim() === '' ? 'Anônimo' : comment.name
			}))
		}

	},
	watch: {
		comments(val) {
			console.log('val', val);
		}

	}
}
</script>

<style>

</style>