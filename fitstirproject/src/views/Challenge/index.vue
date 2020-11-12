<template>
            <div class="container flex flex-col justify-center items-center mx-auto " >
                <div
                        style="background-image: url(https://images.unsplash.com/photo-1538582709238-0a503bd5ae04?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80)"
                        class=" bg-blue-300 h-64 w-24 min-w-full
                rounded-lg shadow-md bg-cover bg-center"
                >
                </div>
                <div class="bg-white -mt-24 shadow-md rounded-lg overflow-hidden">
                    <div class="items-center justify-between py-10 px-5 bg-white shadow-2xl rounded-lg mx-auto text-center">
                        <div class="px-2 -mt-6">
                            <div class="text-center">
                                <h6 class="text-gray-800 text-5xl font-bold">Exercise Challenge</h6>
                                <h2 class="text-gray-800 text-3xl font-bold">
                                    Make Your Day
                                </h2>
                                <h2 class="text-gray-800 text-1xl font-bold">
                                    Real People. Real Videos.
                                </h2>
                                <br>
                                <v-btn
                                        @click="dialog1 = true"
                                        color="error"
                                        x-large
                                >
                                    <v-icon>mdi-play</v-icon>
                                    Create Challenge
                                </v-btn>
                            </div>
                        </div>
                    </div>
                </div>
                <v-dialog
                        v-model="dialog1"
                        max-width="290"
                >
                    <v-card>
                        <v-card-title primary-title>
                            <v-icon
                                    color="primary"
                            >
                                mdi-account</v-icon>
                            Edit Account
                            <v-spacer></v-spacer>
                            <v-btn @click="dialog1 = false" icon text>
                                <v-icon>mdi-close</v-icon>
                            </v-btn>
                        </v-card-title>
                        <v-card-text>




                            <v-col
                                    cols="12"
                                    sm="10"
                                    md="10"
                            >
                                <v-text-field
                                        label="First name"
                                        outlined
                                ></v-text-field>
                            </v-col>
                            <v-col
                                    cols="12"
                                    sm="10"
                                    md="10">
                                <v-text-field
                                        label="First name"
                                        outlined
                                ></v-text-field>
                            </v-col>
                            <v-btn
                                    color="error"
                                    @click=""
                            ><v-icon>mdi-play</v-icon>
                                Create
                            </v-btn>
                        </v-card-text>
                    </v-card>
                </v-dialog>
            </div>

</template>




<script>
    export default {
        name: "index",
        data () {
            return{
                    form:{
                        name:null,
                        image:null,
                        description:null,
                    },
                dialog1: false,
            }
        },
        mounted() {
            this.loadData()
        },
        methods: {
            async loadData() {
                this.user = await this.$store.dispatch('user/getUser')
                this.videoplaylist = await this.$store.dispatch('myplaylist/getMyPlaylist',this.user.pk)
                console.log(this.videoplaylist);
                this.response = true
                console.log(this.user);
            },
            async createvideo() {
                let dataImage = new FormData()
                this.form.user = this.user.pk
                this.form.description = this.user.pk
                let data = await this.$store.dispatch('myplaylist/postMyPlaylist', this.form)
                this.dialog1 = false
                this.loadData()
            },
            async deletePlaylist(){
                let data  = await  this.$store.dispatch('myplaylist/deleteMyPlaylist',this.dataDialog)
                this.dialog = false
                this.dialog2 = false
                this.loadData()
            },
            async getdataDialogid(id){
                this.dialog1 = true
                this.dataDialog= id
            },

        }
    }
</script>

<style scoped>

</style>