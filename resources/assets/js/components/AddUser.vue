<template>
    <div class="row">
        <div class="col-lg-12 mt-4">
            <div class="card card-info">
                <div class="card-header">
                    <h3 class="card-title">Add User</h3>
                </div>
                <form @submit.prevent="createUser" class="form-horizontal">
                    <div class="card-body">
                        <div class="form-group">
                            <label>Name</label>
                            <input v-model="form.name" type="text" name="name"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
                            <has-error :form="form" field="name"></has-error>
                        </div>
                        <div class="form-group">
                            <label>Email</label>
                            <input v-model="form.email" type="email" name="email"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
                            <has-error :form="form" field="email"></has-error>
                        </div>

                        <div class="form-group">
                            <label>Password</label>
                            <input v-model="form.password" type="password" name="password"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                            <has-error :form="form" field="password"></has-error>
                        </div>
                        <div class="form-group">
                            <label>Type</label>
                            <select v-model="form.type" name="type" class="form-control">
                                <option value="">Please Select Role</option>
                                <option value="admin">Admin</option>
                                <option value="user">user</option>
                                <option value="author">Author</option>
                            </select>
                            <has-error :form="form" field="type"></has-error>


                        </div>
                        <div class="form-group">
                            <label>Bio</label>
                            <textarea v-model="form.bio" name="bio"
                                      class="form-control" :class="{ 'is-invalid': form.errors.has('bio') }"></textarea>
                            <has-error :form="form" field="bio"></has-error>
                        </div>

                    </div>
                    <!-- /.card-body -->
                    <div class="card-footer">
                        <button type="submit" class="btn btn-info">Add User</button>
                        <button type="submit" class="btn btn-default float-right">Cancel</button>
                    </div>
                    <!-- /.card-footer -->
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "AddUser",
        data() {
            return {
                // Create a new form instance
                form: new Form({
                    name: '',
                    email: '',
                    password: '',
                    type: '',
                    bio: ''

                })
            }
        },
        methods: {
            createUser() {
                this.$Progress.start();
                this.form.post('api/user').then(response => {
                    this.form.reset();
                    toast({
                        type: 'success',
                        title: 'User created successfully'
                    })
                }).catch(error => {
                    console.log(error)

                })

                this.$Progress.finish();
            }
        }
    }
</script>

<style scoped>

</style>