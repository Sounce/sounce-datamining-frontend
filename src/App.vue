<template>
    <v-app id="app">
        <div>
            <v-toolbar color="#000000" dark class="flex-shrink-1">
                <v-layout align-center justify-center>
                    <v-spacer/>
                    <img src="./assets/sounce-logo.png" height="40px" width="40px"/>
                    <v-spacer/>
                    <v-btn color="#000000" class="mx-auto toolbar-button text-none flex-shrink-1"
                           style="border-bottom: #6F77EF solid">
                        About us
                    </v-btn>
                    <v-spacer/>
                    <v-btn color="#000000" class="mx-auto toolbar-button text-none flex-shrink-1"
                           style="border-bottom: #6F77EF solid">
                        Technologies
                    </v-btn>
                    <v-spacer/>
                    <v-btn color="#000000" class="mx-auto toolbar-button text-none flex-shrink-1"
                           style="border-bottom: #6F77EF solid">
                        Achievements
                    </v-btn>
                    <v-spacer/>
                    <v-btn color="#000000" class="mx-auto toolbar-button text-none flex-shrink-1"
                           style="border-bottom: #6F77EF solid">
                        Contacts
                    </v-btn>
                    <v-spacer/>
                </v-layout>
            </v-toolbar>

            <v-layout justify-center>
                <v-card color="#000000" class="flex-shrink-1">
                    <div>
                        <v-radio-group dark>
                            <v-row>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/thumbs-up.png" height="25px" width="25px"/>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/victory.png" height="25px" width="25px"/>
                                <v-spacer/>
                            </v-row>
                            <v-row>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/splayed-hand.png" height="25px" width="25px"/>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/thumbs-down.png" height="25px" width="25px"/>
                                <v-spacer/>
                            </v-row>
                            <v-row>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/point-up.png" height="25px" width="25px"/>
                                <v-spacer/>
                                <v-radio/>
                                <img src="./assets/emoji-pics/fist.png" height="25px" width="25px"/>
                                <v-spacer/>
                            </v-row>
                        </v-radio-group>
                    </div>
                    <div>
                        <upload-file/>
                    </div>
                    <div>
                      <v-layout justify-center>
                        <v-btn color="#000000" dark>
                          Button for smth
                        </v-btn>
                      </v-layout>
                    </div>
                </v-card>
            </v-layout>

          <v-footer class="pa-3" absolute color="#000000" dark>
            <v-layout justify-center>
              Sounce © {{ new Date().getFullYear() }}. All rights reserved
            </v-layout>
          </v-footer>
        </div>
    </v-app>
</template>

<script>
    import UploadFile from "./components/uploadFile"

    export default {
        name: 'App',

        components: {
            UploadFile,
        },

        data: () => ({
            //
        }),
    }
</script>

<style>
    .toolbar-button {
        font-family: "Noto Sans Condensed Medium";
    }

    #app {
        background-color: #000000;
    }
</style>