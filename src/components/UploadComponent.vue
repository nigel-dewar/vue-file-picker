<template>
  <div class="file">
        <label class="file-label">
            <input
                multiple
                class="file-input"
                type="file"
                @change="uploadImages($event.target.files)"
                :accept="accept"
            >
            <span class="file-cta">
                <span class="file-icon">
                    <i class="fas fa-upload"></i>
                </span>
                <span class="file-label">
                    Choose a file…
                </span>
                
            </span>
        </label>
        <span>
            <p>file names</p>
            <ul>
                <li v-for="name in fileNames" :key="name">{{name}}</li>
            </ul>
            
        </span>
    </div>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    data() {
      return {
        files: [],
        fileNames: [],
        formFiles: []
      }
    },
    props: ["accept", "label", "type", "help", "required"],
    methods: {
      uploadImages(files){

      this.files = files

      console.log(this.files)

      if (this.files) {
        //   let formFiles = [];
        let formData = new FormData();

        for (let file of this.files) {
        
        // this trims a files name so there are no spaces in it
        let trimmedAddress = file.name.split(' ').join('');
            let filename = `${trimmedAddress}`;

            this.fileNames.push(filename);
            
            formData.append("formFiles", file, filename);
        }

        this.formFiles.push(formData)

        this.$emit('changeFiles', this.formFiles)

      }

    }
    },
  })
</script>

<style scoped>

</style>
