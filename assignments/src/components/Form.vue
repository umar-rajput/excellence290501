<template>
    <div class="Form">

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
                                    placeholder="Enter Email Address">
                            </div>
                        </template>
                        <template v-slot:name>
                            <div class="mb-3">
                                <label for="exampleFormControlInput1" class="form-label">Enter Name</label>
                                <input type="text" class="form-control" id="exampleFormControlInput1"
                                    placeholder="Enter Name">
                            </div>
                        </template>
                        <template v-slot:dob>
                            <div class="mb-3">
                                <label for="exampleFormControlInput1" class="form-label">Enter Date of Birth</label>
                                <input type="date" class="form-control" id="exampleFormControlInput1"
                                    placeholder="Enter Date of Birth">
                            </div>
                        </template>
                        <template v-slot:password>
                            <div class="mb-3">
                                <label for="inputPassword5" class="form-label">Enter Password</label>
                                <input type="password" id="inputPassword5" class="form-control"
                                    aria-labelledby="passwordHelpBlock" placeholder="Enter Password">
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
                                <button type="button" class="btn btn-dark" v-on:click="submit">Submit</button>
                            </div>
                        </template>
                    </input-fields>
                </form>
            </div>

        </div>

    </div>
</template>

<script>
import InputFields from './InputFields.vue'

export default {
    name: `Form`,
    components: { InputFields },
    data() {
        return {

        }
    },
}
</script>

<style scoped>
.Form {
    min-height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: radial-gradient(circle, rgba(253, 252, 251, 1) 0%, rgba(226, 209, 195, 1) 100%);
}

.form-main {
    width: 450px;
    border: 1px solid #0000001f;
    border-radius: 20px;
    text-align: left;

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

.btn {
    width: 100%;
}</style>
