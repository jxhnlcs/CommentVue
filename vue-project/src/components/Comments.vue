<template>
<div class="container">
    <h1>Comentários</h1>
    <hr />
    <div class=" form-todo form-group">
        <p>
            <input v-model="name" placeholder="Nome" type="text" name="author"
            class="form-control" />
        </p>
        <p>
        <textarea v-model="message" placeholder="Comentário" name="message" class="form-control"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
    <hr />
    <div class="list-group">
        <div class="list-group-item" v-for="(comment, index) in allComments">
            <span class="comment_author">Autor: <strong>{{comment.name}}</strong></span>
            <p>{{comment.message}}</p>
        <div>
            <a v-on:click.prevent="removeComment(index)" href="#" title="Excluir">Excluir</a>
        </div>
    </div>
</div>
</div>
</template>

<script>
export default{
    data(){
        return {
            comments: [],
            name: '',
            message: ''
        }   
    },
    methods: {
        addComment(){ /* Adiciona o comentário */
            if (this.message.trim() === ''){
                return;
            }

            this.comments.push({
                name: this.name,
                message: this.message
            });

            this.name = '';
            this.message = '';
        },
        removeComment(index){
            this.comments.splice(index, 1);
        }
    },

    computed: {
        allComments(){ /* Se o usuário colocar um comentário sem nome, retorna Anônimo */
            return this.comments.map(comment =>({
                ...comment,
                name: comment.name.trim() === '' ? 'Anônimo' : comment.name
            }))
        }
    },
        watch: {
        comments(val) {
            console.log('val', val)
        }
        }
}
</script>