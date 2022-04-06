<template>     

<div id="uploadFormDiv">
              
            <form id="uploadForm" @submit.prevent="uploadPhoto">
            
                  <div class="form-group">
                      <label for="description">Description</label> <textarea class="form-control" id="description" name="description"></textarea>
                  </div>
                  
                  <div class="form-group">
                      <label for="photo">Photo</label>
                      <input class="form-control" id="photo" name="photo" type="file">
                  </div>
                  <button type="submit" class ="try1" name="submit" id="uploadButton">Submit</button>
            </form>
</div>
</template> 

<script> 

export default {

    data() {       
        return {
            csrf_token: ''
            
        }   
     }, 
    created() {     
         this.getCsrfToken(); 
    }, 

    methods: { 
        uploadPhoto(){   
            let self = this;
            let uploadForm = document.getElementById('uploadForm'); 
            let form_data = new FormData(uploadForm); 


            
            fetch("/api/upload", {     
                method: 'POST' ,
                body: form_data,
                headers: {             
                    'X-CSRFToken': this.csrf_token         
                }  
            }) 
            .then(function(response) {             
                return response.json();           
            })           
            .then(function(data) { 

            console.log(data);
                     
            })
            .catch(function (error) {         
             console.log(error);     
            }); 
        }
        ,   
        getCsrfToken() {     
            let self = this;     
            
            fetch('/api/csrf-token')       
                .then((response) => response.json())       
                .then((data) => {         
                    console.log(data);         
                    self.csrf_token = data.csrf_token;       
                })   
        } 
    }
}
</script>
<style>
body {
    padding-top: 5rem;
    
}


.try1{
    background-color: rgb(48,129,251);
    border-radius: 4px;
    border: none;
    color: white;
    padding: 5px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 18px;
}
.form-group{
    font-size: 18px;
    padding-bottom: 10px;
}
    

p {
    width: 100%;
    text-align: center;
    font-weight: bold;
}
</style>