<template>
  <div class="home">
    <h1>Projects</h1>

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
                <td><a href="#">Delete</a></td>
            </tr>
        </tbody>

    </table>

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
            console.log('Obtem dados da API');
        
            this.$http.get('http://localhost:3000/projects').then(
                (data) => {
                    this.projects = data.body;
                }
            ).catch(
                (error) => {
                    console.log(error);
                }
            );
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
