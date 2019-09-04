<template>
  <div class="home">
    <h2>Project Insert</h2>

    <form @submit.prevent="onSave()">
        Id: <input type="text" name="id" v-model="project.id"> <br>
        Title: <input type="text" name="title" v-model="project.title"> <br>
        <button type="submit">Enviar</button>
    </form>

  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
    name: 'projectForm',
    data () {
        return {
            project: {
                id : '',
                title : ''
            }
        }
    },
    methods: {
        onSave() {
            this.$http.post('http://localhost:3000/projects', this.project).then(
                (data) => {
                    this.$router.push({ name: 'projects' });
                }
            ).catch(
                (error) => {
                    console.log(error);
                }
            );
        },
    },
    mounted () {
        //this.getProjects();
    },
    components: {
        //HelloWorld

    },
}
</script>
