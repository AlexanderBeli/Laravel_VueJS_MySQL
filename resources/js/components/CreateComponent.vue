<script>
import SomeComponent from "./SomeComponent.vue";
export default {
    name: "CreateComponent",
    components: {SomeComponent},

    data() {
        return {
            name: null,
            age: null,
            job: null,
            obj: {
                color: "yellow",
                number: 50,
                isPublished: false
            }
        }
    },

    mounted() {
        this.$parent.$refs.index.indexLog();
    },

    methods: {
        addPerson() {
            axios.post('/api/people',{name:this.name,age:this.age,job:this.job}).then((response) => {
                this.name = null
                this.age = null
                this.job = null
                this.$parent.$refs.index.getPeople();
                // console.log(response);
            })
        }
    }

}
</script>

<template>
    <div class="w-25">
        <div class="mb-3">
            <input type="text" class="form-control" v-model="name" id="name" placeholder="name">
        </div>
        <div class="mb-3">
            <input type="number" class="form-control" v-model="age" id="age" placeholder="age">
        </div>
        <div class="mb-3">
            <input type="text" class="form-control" v-model="job" id="job" placeholder="job">
        </div>
        <div class="mb-3">
            <input @click.prevent="addPerson" class="btn btn-primary" value="Submit">
        </div>
        <SomeComponent :obj="obj"></SomeComponent>
    </div>
</template>

<style scoped>

</style>

