<template>
    <div class="table-add-data">

        <div class="tableAdd">
            <Form v-on:submit-item="submit" v-on:edit-item="edit" v-bind:edit-index="editIndex" v-bind:editEmail="editEmail"
                v-bind:editName="editName" v-bind:editDob="editDob" v-bind:editPassword="editPassword" />
            <table>
                <tr>
                    <th v-for="(item,index) in columns" v-bind:key="index" v-on:click="sortData(index)">{{ item }} ↿⇂</th>
                    <!-- <th>Email</th>
                    <th>Name</th>
                    <th>Date Of Birth</th>
                    <th>Password</th> -->
                    <th>Edit</th>
                    <th>Delete</th>
                </tr>
                <tr v-for="(item, index) in items" v-bind:key="index">
                    <td v-for="(rowitem,rowindex) in item" v-bind:key="rowindex">{{ rowitem }}</td>
                    <!-- <td>{{ item.email }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.dob }}</td>
                    <td>{{ item.password }}</td> -->
                    <td><i class="fa-solid fa-pen-to-square" v-on:click.prevent="editItem(index)"></i></td>
                    <td><i class="fa-solid fa-trash" v-on:click.prevent="deleteItem(index)"></i></td>
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
            editEmail: "",
            editName: "",
            editDob: "",
            editPassword: "",
            editIndex: -1,
            columns:["Email","Name","DOB","Password"],
            sortDesc:false,
            sortKey:"",
        }

    },
    methods: {
        submit: function (editEmail, editName, editDob, editPassword) {
            this.items.push({
                'email': editEmail,
                'name': editName,
                'dob': editDob,
                'password': editPassword,
            });
            this.email = "";
            this.name = "";
            this.dob = "";
            this.password = "";
        },
        deleteItem: function (index) {
            this.items.splice(index, 1);
        },
        editItem: function (index) {
            console.log("Edit index");
            this.editIndex = index;
            this.editEmail = this.items[index];
        },
        edit: function (obj) {
            var { editEmail,editName, editPassword, editDob,editIndex } = obj;
            console.log("actual edit ", editEmail,editName, editPassword, editDob,editIndex);
            this.items[editIndex].email = editEmail;
            this.items[editIndex].name = editName;
            this.items[editIndex].dob = editDob;
            this.items[editIndex].password = editPassword;
            this.editEmail = "";
            this.editName = "";
            this.editDob = "";
            this.editPassword = "";
            this.editIndex = -1;
        },
        sortData: function(index) {
            const key = this.columns[index].toLowerCase().replace(" ", "_");
            console.log(key);
            if (this.sortKey === key) {
                this.sortDesc = !this.sortDesc;
            } else {
                this.sortKey = key;
                this.sortDesc = false;
            }
            console.log("check",this.sortKey==='dob');
            
            this.items.sort((a, b) => {
                const valueA = a[this.sortKey];
                const valueB = b[this.sortKey];
                if (this.sortKey === "dob") {
                    // Convert the date strings to Date objects for comparison
                    const dateA = new Date(valueA);
                    const dateB = new Date(valueB);
                    if (this.sortDesc) {
                        return dateB.getTime() - dateA.getTime();
                    } else {
                        return dateA.getTime() - dateB.getTime();
                    }
                } else {

                    if (this.sortDesc) {
                        return valueB.localeCompare(valueA);
                    } else {
                        return valueA.localeCompare(valueB);
                    }
                }    
            });
            },

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
}
</style>