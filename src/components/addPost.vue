<template>
  <div id='add-post'>
      <h2>Add a Job Post</h2>

      <!--All the input binding will go here-->
      <form>
          <label for="title">Title:</label>
          <input type="text"  v-model.lazy="posting.title" required>
          <label for="content">Content:</label>
          <textarea name="content" id="" cols="30" rows="10"  v-model.lazy="posting.content"></textarea>
          <div id="licenses">
              <label for="None">None</label>
              <input type="checkbox" value="none" v-model="posting.licenses"/>
              <label for="NAR">NAR</label>
              <input type="checkbox" value="NAR" v-model="posting.licenses"/>
              <label for="HCA">HCA</label>
              <input type="checkbox" value="HCA" v-model="posting.licenses"/>
              <label for="NAR">NAC</label>
              <input type="checkbox" value="NAC" v-model="posting.licenses"/>
              <label for="LPN">LPN</label>
              <input type="checkbox" value="LPN" v-model="posting.licenses"/>
              <label for="RN">RN</label>
              <input type="checkbox" value="RN" v-model="posting.licenses"/>
          </div>
          <label for="type">Shift</label>
          <select name="shift" v-model="posting.shift">
              <option v-for="shift in shifts">{{shift}}</option>
          </select>
        
        <button v-on:click.prevent="createPost">Add Post</button>

      </form>

      <div id="preview">
          <h3>Preview Job Post</h3>
          <p>Job Post Title:{{posting.title}}</p>
          <p>Job Post Content:</p>
          <hr>
          <p>{{posting.content}}</p>
          <ul>
              <li v-for="(license, num) in posting.licenses">{{license}}</li>
          </ul>
          <p>Shift:{{posting.shift}} </p>
      </div>

  </div>
</template>

<script>


export default {
  
  data(){
    return{
        posting:{
            title: " ",
            content: " ",
            licenses: [],
            shift: " "
        },

        shifts:['Weekend', 'Day', 'Evening','Graveyard']
        
    }
  }, 
  methods:{
      createPost:function(){
          //const endpoint = 'https://jsonplaceholder.typicode.com/posts';
          console.log("I am here...");
          console.log("this is the posting", this.posting);

          const postBody = {
                userId: 1,
                id: 2,  
                title: this.posting.title,
                body: this.posting.content   
          };

          const data = JSON.stringify(postBody);

          
        fetch("https://jsonplaceholder.typicode.com/posts", {
                  method:"POST",
                  body: data
                  //headers: {"Content-type": "application/json;"},
        }).then(response=>{
            if(response.ok){
                const responseJSON = response.json();
                console.log(responseJSON);
            }
            
            //throw new Error("Request Failed!");
        }).catch(error=>{
            console.log(error);
        });

            
          
      }
  }
}
</script>

<style>
  #add-blog *{
    box-sizing: border-box;
}
#add-blog{
    margin: 20px auto;
    max-width: 500px;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}
h3{
    margin-top: 10px;
}
#licenses input{
    display: inline-block;
    margin-right: 10px;
}
#licenses label{
    display: inline-block;
}
</style>
