<template>
  <div class="uploadFile">
    <div>
      <img src="../assets/infographic.gif" class="gifImage">
    </div>
    <form enctype="multipart/form-data">
        <h1>Upload CSV file</h1>
        <div class="dropbox">
          <input
            type="file"
            multiple
            :name="csvFiles"
            :disabled="isSaving"
            @change="filesChange($event.target.name, $event.target.files);
            fileCount = $event.target.files.length"
            accept=".csv"
            class="input-file"
            id='csvFiles'
          >
        </div>
        <div class="fileList">
          <h2 v-if="uploadedFiles.length> 0">Uploaded File</h2>
          <ol>
            <li class="row" v-for="(files, index) in uploadedFiles" v-bind:key="{index}">
              <h4>{{files.name}}</h4>
              <button class="removeBtn" v-on:click="removeFile">X</button>
            </li>
          </ol>
        </div>
      </form>
  </div>
</template>
<script>
const statusInitial = 0;
// const statusSaving = 1;
// const statusSuccess = 2;
// const statusFailed = 3;
export default {
  name: 'UploadFile',
  data() {
    return {
      title: 'Upload CSV file',
      uploadedFiles: [],
      uploadError: null,
      currentStatus: null,
      uploadedFieldName: 'csv',
      info: null,
    };
  },
  methods: {
    reset: function () {
      this.currentStatus = statusInitial;
      this.uploadedFiles = [];
      this.uploadError = null;
    },
    filesChange: function (fieldName, fileList) {
      // const formData = new FormData();
      if (!fileList.length) return;
      for (let i = fileList.length - 1; i >= 0; i--) {
        this.uploadedFiles.push(fileList[i]);
        // this.save(fileList[i]);
      }
      document.getElementById('csvFiles').value = [];
    },
    removeFile: function (index) {
      this.uploadedFiles.splice(index, 1);
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  text-align: left;
  margin: 0 5px;
}
a {
  color: #42b983;
}
.fileList {
 width: 80%;
 margin: 0 auto;
}
.gifImage {
  height: 400px;
  width: 400px;
}
.removeBtn {
  height: 100%;
  align-self: center;
}
.row {
 display: flex;
 flex-direction: row;
 justify-content: space-between;
}
</style>
