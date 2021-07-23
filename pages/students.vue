<template>
    <div>
        <NavBar />
        <div class="container">
            <h1>Student</h1>
            <div class="row">
                <div class="col-6">
                    <h5>List of Student</h5>
                    <hr>
                    <ul class="list-group">
                        <li class="list-group-item btn-li"  v-for="student in students" :key="student.id" @click="onSelected(student)">
                            {{student.name}} <span class="float-right">{{student.address}}</span>
                        </li>
                    </ul>
                </div>
                <div class="col-4">
                    <studentView :student="selectedstudent" @saved="onChange" @newstudent="onNew" @deleted="onChange" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            students: [],
            selectedstudent: {}
        }
    },
    methods: {
        async getMystudents() {
            await this.$axios.get('/api/students')
            .then((res)=>{
                if(res.status==200) {
                    this.students = res.data
                }
            })
        },
        onChange() {
            this.getMystudents()
            this.selectedstudent = {}
        },
        onSelected(student) {
            this.selectedstudent = student;
        },
        onNew() {
            this.selectedstudent = {}
        },
    },
    created() {
        this.getMystudents()
    }
}
</script>

<style>
.row {
    padding-top: 30px;
}
.container {
    margin-top: 20px;
}
h1 {
    text-align: center;
}
.btn-li {
    cursor: pointer;
}
.btn-li:hover {
    background-color: antiquewhite;
}
</style>