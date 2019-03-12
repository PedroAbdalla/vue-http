<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label>Username</label>
                    <input class="form-control" type="text" v-model="user.username">
                </div>
                <div class="form-group">
                    <label>Mail</label>
                    <input class="form-control" type="text" v-model="user.mail">
                </div>
                <button class="btn btn-primary" @click="submit">Submit</button>
                <hr>
                    <input class="form-control" type="text" v-model="node">
                <hr>
                <button class="btn btn-primary" @click="getData">Get Data</button>
                <br><br>
                <ul class="list-group">
                    <li class="list-group-item" v-for="(u, index) in users" :key="index"> {{u.username}} -- {{u.mail}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            user: {    
                username: '',
                mail: ''
            }, 
            users: [],
            resource: '',
            node: 'data'
        }
    },
    methods: {
        submit() {
            // this.$http.post('data.json', this.user)
            // .then(response => {
            //     console.log(response)
            // }, error => {
            //     console.log(error)
            // })
            // this.resource.save({}, this.user)
            this.resource.SAVEaLL(this.user)
        },
        getData() {
            // this.$http.get('data.json')
            // .then(response => {
            //     return response.json()
            // })
            // .then(data =>  {
            //     const resultArray = [];
            //     for (let key in data) {
            //         resultArray.push(data[key])
            //     }
            //     this.users = resultArray;
            // })
            this.resource.getData({node: this.node})
            .then(response => {
                return response.json()
            })
            .then(data =>  {
                const resultArray = [];
                for (let key in data) {
                    resultArray.push(data[key])
                }
                this.users = resultArray;
            })
        }
    },
    created() {
        const customActions =  {
            SAVEaLL: {method: 'POST', url: 'alternative.json'},
            getData: {method: 'GET', url: 'alternative.json'}
        }
        this.resource = this.$resource('{node}.json', {}, customActions)
    }
}
</script>


<style>
</style>
