<template>
  <div>

    <form>
      <UploadComponent :accept="acceptList" v-on:changeFiles="changeFiles($event)"/>
    </form>

    <button class="button is-primary" @click="submit">Submit</button>
  </div>
</template>

<script>
// import Input from './Input';
import UploadComponent from './UploadComponent';
export default {
  components: {
    // Input
    UploadComponent
  },
  name: "FormComponent",
  props: {
    msg: String
  },
  data() {
    return {

      dataToSubmit: {
        formFiles: []
      },
      // acceptList feeds in props of what type of files the file picker will accept the user to choose from
      // e.g
      // 'application/vnd.openxmlformats-officedocument.wordprocessingml.document' = Word Document
      // 'image/*' = all image types
      // 'image/jpeg' = only jpeg image types
      acceptList: ['application/vnd.openxmlformats-officedocument.wordprocessingml.document', 'image/*']
    }
  },
  methods: {
    // method run when user picks files in the UploadComponent
    changeFiles(e) {
      this.dataToSubmit.formFiles = e;
    },

    submit(){
      console.log(this.dataToSubmit);
    }
  }

  
};
</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->

