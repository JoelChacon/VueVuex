<template>
    <div id="registrations">
        <div class="summary">
            <h3>Registrations</h3>
            <h5>Total: {{ total }}</h5>
        </div>
        <hr>
        <div class="row" v-for="registration in registrations">
            <h4>{{ registration.name }}</h4>
            <span @click="unregister(registration)">(Unregister)</span>
            <div class="date">{{ registration.date }}</div>
        </div>
    </div>
</template>

<script>
    // this is to map the getters from the store
    import { mapGetters } from 'vuex';

    export default {
        methods: {
            unregister(registration) {
                const user = this.$store.state.users.find(user => {
                    return user.id == registration.userId;
                });
                user.registered = false;
                this.$store.state.registrations.splice(this.$store.state.registrations.indexOf(registration), 1);
            }
        },
        computed: {
            ...mapGetters({
                registrations: 'registrations',
                total: 'totalRegistrations'
            })
        }
        //this use the es6 ... spreader, it takes out the properties of the 
        //object and put them in the parent object so you can add for methods
        // computed: {
        //     ...mapGetters({
        //         registrations: 'registrations',
        //         total: 'totalRegistrations'
        //     }),
        //     funky() {
        //         console.log('something');
        //     }
        // }
        // this is the same as below but it's mapped
        // computed: mapGetters({
        //     registrations: 'registrations',
        //     total: 'totalRegistrations'
        // })
        // computed: {
        //     registrations() {
        //         return this.$store.getters.registrations;
        //     },
        //     total() {
        //         return this.$store.getters.totalRegistrations;
        //     }
        // }
    }
</script>

<style scoped>
    #registrations {
        box-shadow: 1px 1px 2px 1px #ccc;
        margin: 20px;
        padding: 20px;
        display: inline-block;
        width: 300px;
        vertical-align: top;
        text-align: left;
    }

    .summary {
        text-align: center;
    }

    .row h4 {
        display: inline-block;
        width: 30%;
        margin: 0 0 10px 0;
        box-sizing: border-box;
    }

    .row span {
        width: 30%;
        color: red;
        cursor: pointer;
    }

    .row span:hover {
        color: darkred;
    }

    .date {
        display: inline-block;
        width: 38%;
        text-align: right;
        box-sizing: border-box;
    }
</style>