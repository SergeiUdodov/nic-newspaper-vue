<template>
  <div>
    <header>
      <div>
        <div v-for="article in articles" :key="article.id">
           <img v-bind:src="article.imageURL">
            <h3>{{article.header}} {{article.date}}</h3>
            <p>{{article.content}}</p>      
            <div v-show="false">{{comments = article.comments}}</div>

                <div v-for="comment in comments" :key="comment.id">
                    {{comment.id}}. {{comment.text}}
                        <div v-show="false">{{user = comment.user}}</div>
                        <p>{{user.firstName}} {{user.lastName}}, {{comment.date}}</p>
                </div>
            <hr />
        </div> 
    </div>
    </header>
  </div>
</template>

<script>
import UserService from "../services/user.service";

export default {
  name: "Home",
  data() {
    return {
      articles:[],
      comments:[],
      user: {}
    };
  },
  mounted() {
    UserService.getPublicContent().then(
      (response) => {
        this.articles = response.data;
      },
      (error) => {
        this.content =
          (error.response &&
            error.response.data &&
            error.response.data.message) ||
          error.message ||
          error.toString();
      }
    );
  },
};
</script>

<style scoped>
    img {  
        max-width: 300px;  
        height: 250px;  
        }
  </style>
