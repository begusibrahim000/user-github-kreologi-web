<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <br>
                <h1>User GITHUB - Kreologi</h1>
                <div class="card">
                    <div class="card-header">
                        <form class="form-inline" @click.prevent="fungsiCariAkunGithub">
                          <input class="form-control" v-model="karakter" type="search" placeholder="Cari akun github" aria-label="Search">
                          <button class="btn btn-outline-success my-2 my-sm-0" type="button">Cari</button>
                        </form>
                    </div>

                    <div class="card-body">
                        <table class="table table-striped">
                          <thead>
                            <tr>
                              <th scope="col">No</th>
                              <th scope="col">Nama</th>
                              <th scope="col">Github</th>
                              <th scope="col">Image</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr v-for="(item,index) in github.items">
                              <th scope="row">{{index + 1 }}</th>
                              <td>{{item.login}}</td>
                              <td>{{item.html_url}}</td>
                              <td><img width="150" height="150" class="img-thumbnail" :src="item.avatar_url" alt=""></td>
                            </tr>
                          </tbody>
                        </table>
                        <!-- {{github}} -->
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    import axios from 'axios'

    export default {
        data() {
            return {
                github: [],
                karakter: ''
            }
        },

        methods: {
            fungsiCariAkunGithub() {
                axios.get(`https://api.github.com/search/users?q=${this.karakter}`)
                .then(response => {
                    this.github = response.data
                })
                .catch(error => console.log(error))
            }
        }
    }
</script>
