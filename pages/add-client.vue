<template>
    <div class="container">
        <div style="padding-top: 3em;">
            <h2>Add Applicant</h2>
            <div class="row">
                <div class="col-md-6" style="padding-left: 1em;">
                    <pii-input field="name">Full name?</pii-input>
                    <pii-input field="filing_court">Court where expungement will be filed.</pii-input>
                    <pii-input field="phone" v-bind:style="phoneStyle">Phone/Cell</pii-input>
                    <pii-input field="email" v-bind:style="phoneStyle">Email</pii-input>

                    <input-date field="dob">Date of birth?</input-date>

                    <pii-input field="notes">Notes?</pii-input>

                </div>
                <div class="col-md-6" style="padding-left: 1em;">
                    <pii-input field="address_line_1">Address Line 1</pii-input>
                    <pii-input field="address_line_2">Address Line 2</pii-input>
                    <pii-input field="city">City?</pii-input>
                    <input-state field="state" style="width: 20em;display: inline-block">State?</input-state>
                    <pii-input field="zip_code"
                               style="width: 10em; display: inline-block; padding-right: 0em;"
                    >Zip?</pii-input>
                </div>
            </div>
        </div>
        <div class="form-group">
            <div class="row">
                <div class="col-md-6">
                    <button v-on:click="add" type="submit" class="btn btn-primary btn-sm">
                        Create
                    </button>
                </div>
                <div class="col-md-6 text-right">
                    <a v-on:click="cancel" class="btn btn-sm btn-default float-right">Cancel</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import PiiInput from "../components/pii-input";
    import InputState from '../components/input-state';
    import InputDate from "../components/input-date";
    export default {
        name: "add-expungie",
       // middleware: 'auth',
        components: {InputDate, PiiInput, InputState},
        mounted() {
            this.$store.dispatch('clearAll');
         },
        data() {
            return {
                zipStyle: {
                    width: '12em'
                },
                phoneStyle: {
                    width: '20em'
                }
            }
        },

        methods: {
            add() {

                this.$store.dispatch('addClient',this.$store.state.client);  // Fix: need to pass the correct client_id
                this.$store.commit('addBlankConviction');
                this.$router.push('/intake')
            },
            cancel() {
                this.$router.push('/clients')
            }
        },
    }
</script>

<style scoped>

</style>
