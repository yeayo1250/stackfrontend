<template>
    <div>
        <button class="btn btn-success float-right" @click="onNew">
            New Student
        </button>
        <h5>List of Student</h5>
        <hr>

        <form action="" @submit.prevent="onSave">
            <b-form-group label="Name">
                <b-form-input v-model="student.name"></b-form-input>
            </b-form-group>
            <b-form-group label="address">
                <b-form-input v-model="student.address"></b-form-input>
            </b-form-group>
            <b-form-group label="age">
                <b-form-input v-model="student.age"></b-form-input>
            </b-form-group>
            <b-form-group label="Date Enrolled">
                <b-form-input type="date" v-model="student.date_enrolled"></b-form-input>
            </b-form-group>
             <b-form-group label="gender"> 
                <b-form-input v-model="student.gender"></b-form-input>
            </b-form-group>
                <button class="btn btn-primary" type="submit">Save Changes</button>
                <button class="btn btn-danger float-right" type="button" @click="onDelete" v-if="student.id">Delete student</button>
        </form>
    </div>
</template>

<script>
export default {
    props: {
        student: {}
    },
    methods: {
        async onSave() {
            try {
                if(!this.student.id) {
                    await this.$axios.post('/api/students', this.student)
                }else{
                    await this.$axios.put('/api/students/' + this.student.id, this.student)
                }

                this.$emit('saved')
            } catch (err) {
                alert(err.response.data.message)
            }
        },
        onNew() {
            this.$emit('newstudent')
        },
        async onDelete() {
            try {
                this.$axios.delete('/api/students/' + this.student.id)
                this.$emit('deleted')
            } catch (err) {
                alert(err.response.data.message)
            }
        }
    }
}
</script>