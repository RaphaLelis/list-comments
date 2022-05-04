<template>
	<div class="container" style="background-color: white;">
		<h1>Comentários</h1>
		<hr/>
		<div class="form-all form-group">
			<p>
				<input placeholder="Nome" type="text" name="author" class="form-control" v-model="name" />
			</p>
			<p>
				<textarea placeholder="Comentário" name="message" class="form-control" v-model="message"></textarea>
			</p>
			<button v-on:click="addComment" type="submit" class="btn btn-primary">Enviar</button>
		</div>
		<hr/>
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
export default {
	data() {
		return {
			comments: [],
			name: '',
			message: ''
		}
	},
	methods: {
		addComment() {
			if (this.message.trim() === '') {
				return;
			}
			this.comments.push({
				name: this.name,
				message: this.message
			});
			this.name = '',
				this.message = ''
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