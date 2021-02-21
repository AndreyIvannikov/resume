<template>
  <div class="container column">
    <form-resume @add-component="addDate"></form-resume>
    <resume-view :elements="elements"></resume-view>
  </div>
  <div class="container">
    <comments-resume
      :data="dataComments"
      @get-comment="getComments"
      :getCommentsError="getCommentsError"
    ></comments-resume>
    <app-loader v-if="loader"></app-loader>
  </div>
</template>

<script>
import CommentsResume from "./components/resume/comments/CommentResume";
import FormResume from "./components/resume/form/FormResume";
import AppLoader from "./components/appLoader/AppLoader";
import ResumeView from "./components/resume/ResumeView";
import axios from "axios";
export default {
  data() {
    return {
      elements: [],
      loader: false,
      dataComments: null,
      getCommentsError: null
    };
  },
  components: {
    CommentsResume,
    FormResume,
    AppLoader,
    ResumeView
  },
  async mounted() {
    const { data } = await axios.get(
      "https://resume-vue-ef8fd-default-rtdb.firebaseio.com/resume.json"
    );
    const dataFirebase = await Object.keys(data).map((item) => {
      return {
        id: item,
        type: data[item].type,
        value: data[item].value
      }
    })
    this.elements = dataFirebase
  },
  methods: {
    async addDate(event) {
      this.elements.push({
        type: event.value,
        value: event.textField
      });
      axios.post(
        "https://resume-vue-ef8fd-default-rtdb.firebaseio.com/resume.json",
        {
          type: event.value,
          value: event.textField
        }
      );
    },
    async getComments() {
      try {
        this.loader = true;
        const { data } = await axios.get(
          "https://jsonplaceholder.typicode.com/comments?_limit=42"
        );

        if (!data) {
          throw new Error("Ошибка");
        }

        this.getCommentsError = null;
        this.loader = false;
        this.dataComments = await data;
      } catch (e) {
        this.loader = false;
        this.getCommentsError = e.message;
      }
    }
  },
  computed: {
    isLengthTextarea() {
      return this.textField.length < 3;
    }
  }
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
