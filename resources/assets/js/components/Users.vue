<template>
    <div class="row">
        <div class="col-lg-12 mt-4">
            <div class="card">
                <div class="card-header">
                    <h3 class="card-title">Users</h3>

                    <div class="card-tools">
                        <router-link to="/add_user">
                            <button type="submit" class="btn btn-sm btn-success"><i class="fa fa-plus"></i> Add New
                            </button>
                        </router-link>
                    </div>
                </div>
                <!-- /.card-header -->
                <div class="card-body table-responsive p-0">
                    <table class="table table-hover">
                        <tbody>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Email</th>
                            <th>Type</th>
                            <th>Register At</th>
                            <th>Action</th>
                        </tr>
                        <tr v-for="user in users" :key="user.id">
                            <td>{{ user.id }}</td>
                            <td>{{ user.name }}</td>
                            <td>{{ user.email }}</td>
                            <td>{{ user.type | capitalize }}</td>
                            <td>{{ user.created_at | dateFormat}}</td>
                            <td>
                                <button class="btn btn-sm btn-info"><i class="fa fa-pencil-square-o"></i></button>
                                <button @v-popover:myname class="btn btn-sm btn-danger" @click="deleteUser(user.id)"><i
                                        class="fa fa-trash-o"></i></button>
                                <popover name="myname">
                                    Hello!
                                </popover>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                </div>
                <!-- /.card-body -->
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Users",
        data() {
            return {
                users: {}
            }
        },
        methods: {
            loadUsers() {
                axios.get("api/user").then(({data}) => {
                    this.users = data.data
                })
            },
            deleteUser(id) {
                axios.delete("api/user/"+id).then(({data}) => {
                    this.users = data.data
                })
            }
        },
        created() {
            this.loadUsers();
            console.log("User Coponet");
        }
    }
</script>

<style scoped>

</style>