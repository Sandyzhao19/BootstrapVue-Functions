<template>
  <div>
    <b-row>
      <b-col cols="12">
        <p>
          Username
          <span class="required-star" style="color: #ea4c89; margin-left: 5px"
            >*</span
          >
        </p>
        <b-form-input
          v-model="usernameKeyword"
          placeholder="Search Username"
          @input="searchUsername"
        ></b-form-input>
        <p
          v-if="
            this.searchUsernameResults === null ||
            this.searchUsernameResults?.length === 0
          "
          style="color: #ea4c89; font-size: 14px; padding: 5px 0 0 5px"
        >
          Username Required
        </p>

        <div v-if="showUsernameResult" class="username-result-container">
          <b-list-group v-if="searchUsernameResults.length > 0">
            <b-list-group-item
              v-for="(result, index) in searchUsernameResults"
              :key="index"
              @click="selectUsername(result)"
              class="username-result-item"
            >
              {{ result.username }}
            </b-list-group-item>
          </b-list-group>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "FuzzySearchBar",
  data() {
    return {
      usernames: ["John", "Jane", "Michael", "Emily", "David", "Sarah"],
      selectedUser: {
        userID: null,
        username: null,
      },
      usernameKeyword: "",
      showUsernameResult: false,
      searchUsernameResults: null,
    };
  },
  methods: {
    searchUsername() {
      if (this.usernameKeyword) {
        this.showUsernameResult = true;
        const keywords = this.usernameKeyword.toLowerCase().split(/[\s()]+/);
        this.searchUsernameResults = this.usernames.filter((username) => {
          const usernameName = username.usernameName.toLowerCase();
          return keywords.every((keyword) => usernameName.includes(keyword));
        });
        if (this.searchUsernameResults.length === 0) {
          this.selectedUser = {
            userID: null,
            username: null,
          };
        }
      } else {
        this.searchUsernameResults = null;
      }
    },

    selectUsername(user) {
      this.selectedUser.userID = user.userID;
      this.selectedUser.username = user.usernameName;
      this.usernameKeyword = this.selectedUser.username;
      this.showUsernameResult = false;
    },
  },
};
</script>

<style>
.username-result-container {
  max-height: 170px;
  overflow-y: auto;
}

.username-result-item:hover {
  background-color: #f0f0f0 !important;
  cursor: pointer;
}
</style>
