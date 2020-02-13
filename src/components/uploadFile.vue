<template>
    <v-container>
        <v-card dark width="400" min-height="300" @drop.prevent="addFileFromDrag" @dragover.prevent
                @click="handleClick">
                <!--
                Undisplayed file input that is used to upload files on click.
                (When user clicks on the card - the method handleClick() performs
                a click on that input element which opens file dialog).
                -->
            <input type="file" id="file-picker" accept="image/png, image/jpeg"
                   style="display: none" @change="addFileFromInput"/>
            <div id="box-text">
                To upload an image drag it onto this box or click the box to pick a photo from your device
            </div>
            <v-img v-if="imgAvailable" :src="url"/>
        </v-card>
        <v-card v-if="imgAvailable" dark width="400">
            <v-card-actions>
                <v-layout justify-center>
                    <v-spacer/>
                    <v-btn @click="uploadFile">
                        Upload
                    </v-btn>
                    <v-spacer/>
                    <v-btn @click="cancel">
                        Cancel
                    </v-btn>
                    <v-spacer/>
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
            // Url to the file field which is used in v-img to display the
            // uploaded image
            url: '',
            // Defines whether the image is already uploaded - required for
            // showing/hiding some elements
            imgAvailable: false,
        }),

        methods: {
            addFileFromDrag(e) {
                this.imgAvailable = false

                let droppedFiles = e.dataTransfer.files

                if (!this.validateFile(droppedFiles)) return;

                this.file = droppedFiles[0]
                this.url = URL.createObjectURL(this.file)
                this.imgAvailable = true
            },

            // method called on click to open file dialog
            handleClick() {
                if(this.imgAvailable) return
                document.getElementById('file-picker').click()
            },

            addFileFromInput(e) {
                if (this.disableClick) return
                this.imgAvailable = false

                let files = e.target.files

                if (!this.validateFile(files)) return;

                this.file = files[0]
                this.url = URL.createObjectURL(this.file)
                this.imgAvailable = true
            },

            cancel() {
                // nullifies the value in the input element so that user can upload again
                // the image he cancelled
                document.getElementById('file-picker').value = null
                this.file = ''
                this.imgAvailable = false
            },


            // method for uploading file - to be edited later, now simply
            // makes post request on httpbin.org and shows result.
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
            },

            // utility method for validating the file obtained from the user
            validateFile(droppedFiles) {
                if (!droppedFiles) {
                    alert("Something went wrong, couldn't find any file!")
                    return false;
                }

                if (droppedFiles.length > 1) {
                    alert("Please upload only one file!")
                    return  false;
                }

                if (!droppedFiles[0].name.endsWith(".jpg") && !droppedFiles[0].name.endsWith(".png")) {
                    alert("Please only upload image files (supported formats: JPG, PNG!)")
                    return  false;
                }

                if (droppedFiles[0].size > 10*1024*1024) {
                    alert("Please upload a file of viable size (not more than 10 MB!)")
                    return false;
                }

                return true
            }

        }
    }
</script>

<style scoped>

    .rounded-card {
        border-radius: 50px;
    }

    #box-text {
        color: #BBBBBB;
        font-size: 14px
    }

</style>