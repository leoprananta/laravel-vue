<template>
    <div class="container mt-3">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card card-default">
                    <div class="card-header">TAMBAH POST</div>

                    <div class="card-body">

                        <form @submit.prevent="PostStore">

                            <div class="form-group">
                                <label>TITLE</label>
                                <input type="text" class="form-control" v-model="post.title"
                                       placeholder="Masukkan Title">
                                <div v-if="validation.title">
                                    <div class="alert alert-danger mt-1" role="alert">
                                        {{ validation.title[0] }}
                                    </div>
                                </div>
                            </div>


                            <div class="form-group">
                                <label>DESCRIPTION</label>
                                <textarea class="form-control" v-model="post.description" rows="5"
                                          placeholder="Masukkan Deskripsi"></textarea>
                                <div v-if="validation.description">
                                    <div class="alert alert-danger mt-1" role="alert">
                                        {{ validation.description[0] }}
                                    </div>
                                </div>
                            </div>


                            <div class="form-group">
                                <button type="submit" class="btn btn-md btn-success">SIMPAN</button>
                                <button type="reset" class="btn btn-md btn-danger">RESET</button>
                            </div>


                        </form>


                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        data() {
            return {
                post: {},
                validation: []
            }
        },
        methods: {
            PostStore() {
                let uri = 'http://localhost:8000/api/post/store';
                this.axios.post(uri, this.post)
                    .then((response) => {
                        this.$router.push({
                            //dir name
                            name: 'posts'
                        });
                    })
                    .catch(error => {
                    this.validation = error.response.data.data;
                });
            }
        }
    }
</script>