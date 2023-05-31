<template>
    <div class="Form">
        <div class="ragisterHere">
            <h2>Click here to Ragister!!</h2>
            <button v-on:click="()=> TogglePopup('buttonTrigger')" class="register btn btn-dark">Register</button>
        </div>

        <PopUp v-if="popupTrigger.buttonTrigger" :TogglePopup="
                ()=>TogglePopup('buttonTrigger')">

            
            <div class="form-main">
                <header>
                    <h3>Form</h3>
                </header>
                
                <div class="inputs">
                    <form v-on:submit.prevent>
                        <input-fields>
                        <template v-slot:email>
                            <div class="mb-3">
                                <label for="exampleFormControlInput1" class="form-label">Enter Email Address</label>
                                <input type="email" class="form-control" id="exampleFormControlInput1"
                                placeholder="Enter Email Address" v-model="email">
                            </div>
                        </template>
                        <template v-slot:name>
                            <div class="mb-3">
                                <label for="exampleFormControlInput1" class="form-label">Enter Name</label>
                                <input type="text" class="form-control" id="exampleFormControlInput1"
                                    placeholder="Enter Name" v-model="name">
                            </div>
                        </template>
                        <template v-slot:dob>
                            <div class="mb-3">
                                <label for="exampleFormControlInput1" class="form-label">Enter Date of Birth</label>
                                <input type="date" class="form-control" id="exampleFormControlInput1"
                                placeholder="Enter Date of Birth" v-model="dob">
                            </div>
                        </template>
                        <template v-slot:password>
                            <div class="mb-3">
                                <label for="inputPassword5" class="form-label">Enter Password</label>
                                <input type="password" id="inputPassword5" class="form-control"
                                aria-labelledby="passwordHelpBlock" placeholder="Enter Password" v-model="password">
                                <div id="passwordHelpBlock" class="form-text">
                                    Your password must be 8-20 characters long, contain letters and numbers, and must not
                                    contain
                                    spaces, special characters.
                                </div>
                            </div>
                        </template>
                        <template v-slot:confirm>
                            <div class="mb-3">
                                <label for="inputPassword5" class="form-label">Confirm Password</label>
                                <input type="password" id="inputPassword5" class="form-control"
                                    aria-labelledby="passwordHelpBlock" placeholder="Confirm Password">
                            </div>
                        </template>
                        <template v-slot:checkbox>
                            <div class="input-group mb-3 align-items-center">
                                <input type="checkbox" class="me-2">
                                <span>Accept the
                                    <a href="">terms and condition</a>
                                </span>
                            </div>
                        </template>
                        <template v-slot:submit>
                            <div class="submit-button">
                                <button type="button" class="btn1 btn btn-dark" v-on:click="submit">Submit</button>
                            </div>
                        </template>
                    </input-fields>
                </form>
            </div>
            
        </div>
    </PopUp>

    </div>
</template>

<script>
import InputFields from './InputFields.vue';
import PopUp from './PopUp.vue';
import { ref } from 'vue';

export default {
    name: `Form`,
    components: {InputFields,PopUp},
    data() {
        const popupTrigger=ref({
            buttonTrigger:false,
            timedTrigger:false
        });
        const TogglePopup=(trigger)=>{
            popupTrigger.value[trigger]=!popupTrigger.value[trigger]
        };
        return {
            email:"",
            name:"",
            password:"",
            dob:"",
            // items:[],
            popupTrigger,
            TogglePopup,

        }
    },
    watch:{
        editEmail:function(newEmail){
            console.log("watch ",newEmail.email,newEmail.name,newEmail.dob,newEmail.password);
            this.email=newEmail.email;
            this.name=newEmail.name;
            this.dob=newEmail.dob;
            this.password=newEmail.password;
            // console.log(newEmail.email);
        }
    },
    props:{
        editEmail:{type:String,require:true},
        // editName:{type:String,require:true},
        // editDob:{type:String,require:true},
        // editPassword:{type:String,require:true},
        editIndex:{type:Number,require:true}
    },
    methods:{
        submit:function(){
            console.log("Entered value ",this.email,this.name,this.dob,this.password, this.editIndex);
            if(this.editIndex!== -1){
                console.log("edit item");
                this.$emit("edit-item",{
                    editEmail:this.email,
                    editName:this.name,
                    editDob:this.dob,
                    editPassword:this.password,
                    editIndex:this.editIndex,
                });
            }else{
                this.$emit("submit-item", this.email,this.name,this.dob,this.password);
            }
            this.email="";
            this.name="";
            this.dob="";
            this.password="";
        },
        arrange(){
            console.log("arrange");
            return alert("arrange");
        },
        // handlePromptClick(){
        //     Swal
        // }
    }
}
</script>

<style scoped>
/* .Form {
    min-height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: radial-gradient(circle, rgba(253, 252, 251, 1) 0%, rgba(226, 209, 195, 1) 100%);
} */

.form-main {
    width: 450px;
    background: #fff;
    border: 1px solid #0000001f;
    border-radius: 20px;
    text-align: left;
    box-shadow: 2px 2px 6px 1px rgba(0,0,0,0.75);
}

.form-main header {
    text-align: center;
    margin: 15px 0px;
}

.inputs {
    overflow-y: scroll;
    height: 380px;
    padding: 0px 30px;
    margin: 30px 0px;
}

::-webkit-scrollbar {
    display: none;
}

.btn1 {
    width: 100%;
}

</style>
