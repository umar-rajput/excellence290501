<template>
    <div class="table-add-data">

        <div class="tableAdd">
            <Form v-on:submit-item="submit" v-bind:email="email" v-bind:name="name" v-bind:dob="dob"
                v-bind:password="password" />
            <table>
                <tr>
                    <th>Email</th>
                    <th>Name</th>
                    <th>Date Of Birth</th>
                    <th>Password</th>
                </tr>
                <tr v-for="(item, index) in items" v-bind:key="index">
                    <td>{{ item.email }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.dob }}</td>
                    <td>{{ item.password }}</td>
                </tr>
            </table>
        </div>

    </div>
</template>

<script>

import Form from './Form.vue'

export default {
    name: 'TableAddData',
    components: { Form },
    data() {
        return {
            items: [],
            // email:"",
        }

    },
    methods: {
        submit: function (email, name, password, dob) {
            this.items.push({
                'email': email,
                'name': name,
                'password': password,
                'dob': dob
            });
            this.email = "";
            this.name = "";
            this.dob = "";
            this.password = "";
        }
    }
}
</script>

<style scoped>
.tableAdd {
    min-height: 100vh;
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    align-items: center;
    background: radial-gradient(circle, rgba(253, 252, 251, 1) 0%, rgba(226, 209, 195, 1) 100%);
}

table {
    width: 85%;
    margin: 15px 65px;
    padding: 6px;
}

table,
tr,
td,
th {
    border: 1px solid #000;
    border-collapse: collapse;
}</style>