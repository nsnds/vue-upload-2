<template>
  <div class="upload-box">
    <form method="post" enctype="multipart/form-data" ref="form">
      <div class="upload-row" v-for="(i, idx) in files" :key="idx" v-if="files.length > 0">
        <input type="text" disabled v-model="i.text">
        <input type="file" hidden :id="`upIpt${idx}`" @change="handleFileChange">
        <label :for="`upIpt${idx}`">上传文件</label>
        <span class="btn" v-if="idx === 0" @click="add(idx)">&#43;</span>
        <span class="btn" v-else @click="minus(idx)">&minus;</span>
    </div>
    </form>
  </div>
</template>

<script>
import $ from 'jquery'
import 'jquery-form'

export default {
  name: 'upload',
  props: {
    files: {
      default () {
        return [{text: ''}]
      },
      type: Array
    }
  },
  data () {
    return {
    }
  },
  created () {
  },
  methods: {
    handleFileChange (e) {
      console.log('file change!!!')

      let _this = this
      let form = this.$refs.form
      let file = e.target
      let idx = parseInt(file.getAttribute('id').substr(5))

      if (file.files[0] === undefined) {
        this.files[idx].text = ''
        return
      }

      file.setAttribute('name', 'file')

      $(form).ajaxSubmit({
        url: 'http://localhost:3000/upload/file',
        type: 'post',
        success (data) {
          if (data.code === 0) {
            console.log('OK')
            _this.files[idx].text = file.files[0].name
          }
        },
        error (err) {
          console.log(err)
        }
      })

      file.setAttribute('name', '')
    },
    add () {
      this.files.push({text: ''})
    },
    minus (idx) {
      this.files.splice(idx, 1)
    }
  },
  watch: {
    files: {
      handler: function (n, o) {
        this.$emit('changeFile', n)
      },
      deep: true
    }
  }
}
</script>

<style>
.upload-row {
  overflow: hidden;
  margin-top: 5px;
}
.upload-row:first-child {
  margin-top: 0;
}
.upload-row input[type=text] {
  display: inline-block;
  height: 32px;
  border-radius: 5px;
  border: 1px solid #e4e7ed;
  font-size: 14px;
  outline:none;
  transition: border 0.4s;
  text-indent: 5px;
}
.upload-row input[type=text]:focus {
  transition: border 0.4s;
  border-color: #409eff;
}
.upload-row label {
  vertical-align: middle;
  border-radius: 5px;
  border: 1px solid #b3d8ff;
  padding: 8px 20px;
  font-size: 14px;
  background-color: #ecf5ff;
  color: #409eff;
  display: inline-block;
}
.upload-row .btn {
  display: inline-block;
  width: 35px;
  height: 35px;
  vertical-align: middle;
  background: #fef0f0;
  background-size: 32px 32px;
  border: 1px solid #e4e7ed;
  border-radius: 5px;
  line-height: 37px
}
</style>
