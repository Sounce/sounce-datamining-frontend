<template>
    <v-container>
        <v-card dark width="400" min-height="300" @drop.prevent="addFile" @dragover.prevent>
            <v-card-title>
                To upload your image drop it in this box
            </v-card-title>
            <v-img v-if="imgAvailable" :src="url">
                <v-layout v-if="imgAvailable" align-start justify-end>
                    <v-btn small color="red" dark @click="cancel">
                        X
                    </v-btn>
                </v-layout>
            </v-img>
            <v-card-actions v-if="imgAvailable">
                <v-layout justify-center>
                    <v-btn @click="uploadFile">
                        Upload
                    </v-btn>
                </v-layout>
            </v-card-actions>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "uploadFile",

        data: () => ({
            file: '',
            url: '',
            imgAvailable: false
        }),

        methods: {
            addFile(e) {
                this.imgAvailable = false
                let droppedFiles = e.dataTransfer.files
                if (!droppedFiles) {
                    alert("Something went wrong, couldn't find any file!")
                    return
                }

                if (droppedFiles.length > 1) {
                    alert("Please upload only one file!")
                    return
                }

                if (!droppedFiles[0].name.endsWith(".jpg") && !droppedFiles[0].name.endsWith(".png")) {
                    alert("Please only upload image files (supported formats: JPG, PNG!)")
                    return
                }

                if (droppedFiles[0].size > 10*1024*1024) {
                    alert("Please upload a file of viable size (not more than 10 MB!)")
                }

                this.file = droppedFiles[0]
                this.url = URL.createObjectURL(this.file)
                this.imgAvailable = true
            },

            cancel() {
                this.file = ''
                this.imgAvailable = false
            },

            uploadFile() {
                let formData = new FormData()
                // this.files.forEach((f, x) => {
                //     formData.append('file', f)
                // })

                formData.append('file', this.file)

                fetch('https://httpbin.org/post', {
                    method: 'POST',
                    body: formData
                })
                    .then(res => res.json())
                    .then(res => {
                        // eslint-disable-next-line no-console
                        console.log('done uploading', res)
                    })
                    .catch(e => {
                        // eslint-disable-next-line no-console
                        console.error(JSON.stringify(e.message))
                    })
            }

        }
    }
</script>

<style scoped>

</style>