<template>
  <div class="home">
    <h1>Projects</h1>

    <router-link :to="{name: 'projectInsert'}">Inserir</router-link>

    <table>
        <thead>
            <tr>
                <td>ID</td>
                <td>Title</td>
                <td>Actions</td>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(project, index) in projects" :key="index">
                <td>{{ project.id }}</td>
                <td>{{ project.title }}</td>
                <td><a href="#">Edit</a></td>
                <td><a href="#" @click="deleteProject(project.id)">Delete</a></td>
            </tr>
        </tbody>

    </table>

    <router-view name="children"/>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
    name: 'projects',
    data () {
        return {
            projects: []
        }
    },
    methods: {
        getProjects() {
            this.$http.get('http://localhost:3000/projects').then(
                (data) => {
                    this.projects = data.body;
                }
            ).catch(
                (error) => {
                    console.log(error);
                }
            );
        },
        deleteProject(id) {
            if (!confirm("Deseja deletar o registro?")) {
                return ;
            }

            this.$http.delete('http://localhost:3000/projects/'+id).then(
                (data) => {
                    alert('Deletado id ' + id);
                    this.getProjects();
                }
            )
        } 
    },
    mounted () {
        this.getProjects();
    },
    components: {
        //HelloWorld

    },
}
</script>
