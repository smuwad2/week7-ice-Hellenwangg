<script>
import axios from "axios";

export default {
  data() {
    return {
      moods: ["Happy", "Sad", "Angry"],
      selMood: "",
      subject: "",
      entry: "",
      outputMsg: "",
    };
  },

  computed: {
    baseUrl() {
      // if running locally (e.g. localhost:5173 or similar)
      if (window.location.hostname === "localhost") {
        return "http://localhost:3000"; // adjust if your Express server runs on a different port
      }
      return `${window.location.protocol}//${window.location.host}`;
    },
  },

  methods: {
    addPost() {
      axios
        .get(`${this.baseUrl}/addPost`, {
          params: {
            subject: this.subject,
            entry: this.entry,
            mood: this.selMood,
          },
        })
        .then((response) => {
          this.outputMsg = response.data.message;
        })
        .catch((error) => {
          console.error(error);
          this.outputMsg = "Error adding post.";
        });
    },
  },
};
</script>

<template>
  <div class="table m-2">
    <h3>Add a New Blog Post</h3>

    <div>
      Subject:
      <input type="text" size="30" v-model="subject" required />
    </div>

    <div>
      Entry:
      <br />
      <textarea
        name="entry"
        cols="80"
        rows="5"
        v-model="entry"
        required
      ></textarea>
    </div>

    <div>
      Mood:
      <select v-model="selMood" required>
        <option disabled value="">-- Select mood --</option>
        <option v-for="mood in moods" :key="mood" :value="mood">
          {{ mood }}
        </option>
      </select>
    </div>

    <br />
    <button @click="addPost">Submit New Post</button>
    <br /><br />
    {{ outputMsg }}
    <hr />
    Click <router-link to="/ViewPosts/">here</router-link> to return to Main Page
  </div>
</template>
