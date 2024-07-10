<template>
  <div class="container mt-5">
      <form>
          <div class="row mb-3">
              <div class="col-md-6">
                  <label for="pageTitle" class="form-label">Page Title</label>
                  <input type="text"
                         class="form-control" 
                         v-model="pageTitle"
                         id="pageTitle" 
                         placeholder="Enter page title">
              </div>
              <div class="col-md-6">
                  <label for="linkText" class="form-label">Link Text</label>
                  <input type="text" 
                         v-model="linkText" 
                         class="form-control" 
                         id="linkText" 
                         placeholder="Enter link text">
              </div>
          </div>
          <div class="row mb-3">
              <div class="col-md-6">
                  <label for="content" class="form-label">Content</label>
                  <textarea class="form-control" 
                            v-model="pageContent" 
                            id="content" 
                            rows="3" 
                            placeholder="Enter content"></textarea>
              </div>
              <div class="col-md-6">
                  <label for="linkUrl" class="form-label">Link URL</label>
                  <input type="url"
                         class="form-control" 
                         v-model="linkUrl"
                         id="linkUrl" 
                         placeholder="Enter link URL">
              </div>
          </div>
          <div class="row mb-3">
              <div class="col-md-6">
                  <button type="submit"
                          class="btn btn-primary"
                          @click.prevent="submitForm"
                          :disabled="!isFormValid"
                          >Create Page</button>
              </div>
              <div class="col-md-6 d-flex align-items-center">
                  <div class="form-check">
                      <input class="form-check-input" 
                             type="checkbox" 
                             id="published"
                             v-model="published">
                      <label class="form-check-label" for="published">Published</label>
                  </div>
              </div>
          </div>
      </form>
  </div>
  </template>
  
<script>
import { watch } from 'vue';

  export default {
    props : ["pageCreated"],
    computed : {
      isFormValid(){
        return this.pageTitle && this.pageContent && this.linkText && this.linkUrl
      }
    },
    data() {
      return {
        pageTitle: '',
        pageContent: '',
        linkText: '',
        linkUrl: '',
        published: false
      };
    },
    methods: {
      submitForm(){
        if (!this.pageTitle || !this.pageContent || !this.linkText || !this.linkUrl) {
          alert('Please fill in all fields');
          return;
        }
        this.pageCreated({
          pageTitle : this.pageTitle,
          pageContent : this.pageContent,
          link : {
            text : this.linkText, 
            url : this.linkUrl, 
          },
          published : this.published  
        });
      }
  },
  watch : {
    pageTitle(newTitle, oldTitle){
      if (this.linkText === oldTitle) {
        this.linkText = newTitle;
      }
    },
    linkText(newText, oldText){
      if (this.linkUrl !== newText) {
        this.linkUrl = newText.toLowerCase().replace(" ", "") + ".html";
      }
    }
  }
};
</script>
