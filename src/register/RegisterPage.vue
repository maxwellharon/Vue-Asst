<template>
    <div>
        <h2>Register</h2>
        <form @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="fullName">Full Name</label>
                <input type="text" v-model="user.firstName" v-validate="'required'" name="fullName" class="form-control" :class="{ 'is-invalid': submitted && errors.has('firstName') }" />
                <div v-if="submitted && errors.has('fullName')" class="invalid-feedback">{{ errors.first('fullName') }}</div>
            </div>
            <div class="form-group">
                <label for="idNo">ID Number</label>
                <input type="integer" v-model="user.idNumber" v-validate="'required'" name="ID Number" class="form-control" :class="{ 'is-invalid': submitted && errors.has('idNumber') }" />
                <div v-if="submitted && errors.has('idNumber')" class="invalid-feedback">{{ errors.first('idNumber') }}</div>
            </div>
            <div class="form-group">
                <label for="mobileNumber">Mobile Number</label>
                <input type="integer" v-model="user.mobileNumber" v-validate="'required'" name="mobileNumber" class="form-control" :class="{ 'is-invalid': submitted && errors.has('mobileNumber') }" />
                <div v-if="submitted && errors.has('mobileNumber')" class="invalid-feedback">{{ errors.first('mobileNumber') }}</div>
            </div>
            <div class="form-group">
                <label for="emailAddress">Email Address</label>
                <input type="text" v-model="user.email" v-validate="'required'" name="emailAddress" class="form-control" :class="{ 'is-invalid': submitted && errors.has('emailAddress') }" />
                <div v-if="submitted && errors.has('emailAddress')" class="invalid-feedback">{{ errors.first('emailAddress') }}</div>
            </div>
            <div class="form-group">
                <label for="profileUrl">Profile Url</label>
                <input type="text" v-model="user.profileUrl" v-validate="'required'" name="profileUrl" class="form-control" :class="{ 'is-invalid': submitted && errors.has('profileUrl') }" />
                <div v-if="submitted && errors.has('profileUrl')" class="invalid-feedback">{{ errors.first('profileUrl') }}</div>
            </div>
            <div class="form-group">
                <label for="username">Username</label>
                <input type="text" v-model="user.userName" v-validate="'required'" name="userName" class="form-control" :class="{ 'is-invalid': submitted && errors.has('userName') }" />
                <div v-if="submitted && errors.has('userName')" class="invalid-feedback">{{ errors.first('userName') }}</div>
            </div>
            <div class="form-group">
                <label htmlFor="password">Password</label>
                <input type="password" v-model="user.password" v-validate="{ required: true, min: 6 }" name="password" class="form-control" :class="{ 'is-invalid': submitted && errors.has('password') }" />
                <div v-if="submitted && errors.has('password')" class="invalid-feedback">{{ errors.first('password') }}</div>
            </div>
            <div class="form-group">
                <button class="btn btn-primary" :disabled="status.registering">Register</button>
                <img v-show="status.registering" src="data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA==" />
                <router-link to="/login" class="btn btn-link">Cancel</router-link>
            </div>
        </form>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            user: {
                fullName: '',
                idNO: '',
                mobileNumber: '',
                emailAddress: '',
                profileUrl: '',
                userName: '',
                password: ''
            },
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    methods: {
        ...mapActions('account', ['register']),
        handleSubmit(e) {
            this.submitted = true;
            this.$validator.validate().then(valid => {
                if (valid) {
                    this.register(this.user);
                }
            });
        }
    }
};
</script>