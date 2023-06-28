<template>
  <div>
    <b-row>
      <b-col cols="12" v-if="!isTitleEditing">
        <b-row>
          <b-col cols="11">
            <h3 class="title" @click="toggleTitleEdit">
              {{ title }}
            </h3>
          </b-col>
          <b-col cols="1">
            <b-link>
              <b-icon
                class="mt-2"
                icon="pencil-fill"
                scale="1.5"
                @click="toggleTitleEdit"
              ></b-icon>
            </b-link>
          </b-col>
        </b-row>
      </b-col>

      <b-col cols="12" v-else>
        <b-form @submit.stop="saveTitleChanges">
          <b-row>
            <b-col cols="10">
              <b-form-input v-model="editedTitle" ref="titleInput" />
            </b-col>
            <b-col cols="1">
              <b-link>
                <b-icon
                  class="icon mt-2"
                  icon="check-lg"
                  scale="1.5"
                  @click="saveTitleChanges"
                ></b-icon>
              </b-link>
            </b-col>
            <b-col cols="1">
              <b-link>
                <b-icon
                  class="icon mt-2"
                  icon="x-lg"
                  scale="1.5"
                  @click="cancelTitleChanges"
                ></b-icon>
              </b-link>
            </b-col>
          </b-row>
        </b-form>
      </b-col>
    </b-row>

    <b-row class="mt-3 pb-4">
      <b-col cols="12" v-if="!isDescriptionEditing">
        <b-row>
          <b-col cols="11">
            <p class="description" @click="toggleDescriptionEdit">
              {{ description }}
            </p>
          </b-col>
          <b-col cols="1">
            <b-link>
              <b-icon
                class="icon mt-2"
                icon="pencil-fill"
                scale="1.5"
                @click="toggleDescriptionEdit"
              ></b-icon>
            </b-link>
          </b-col>
        </b-row>
      </b-col>

      <b-col cols="12" v-else>
        <b-form @submit.stop="saveDescriptionChanges">
          <b-row>
            <b-col cols="10">
              <b-form-input
                v-model="editedDescription"
                ref="descriptionInput"
              />
            </b-col>
            <b-col cols="1">
              <b-link>
                <b-icon
                  class="icon mt-2"
                  icon="check-lg"
                  scale="1.5"
                  @click="saveDescriptionChanges"
                ></b-icon>
              </b-link>
            </b-col>
            <b-col cols="1">
              <b-link>
                <b-icon
                  class="icon mt-2"
                  icon="x-lg"
                  scale="1.5"
                  @click="cancelDescriptionChanges"
                ></b-icon>
              </b-link>
            </b-col>
          </b-row>
        </b-form>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "SingleFieldInlineEdit",
  data() {
    return {
      title: "Untitled",
      isTitleEditing: false,
      editedTitle: "",

      description: "Add Description",
      isDescriptionEditing: false,
      editedDescription: "",
    };
  },
  methods: {
    toggleTitleEdit() {
      this.isTitleEditing = true;
      this.editedTitle = this.title;
      this.$nextTick(() => {
        this.$refs.titleInput.focus();
      });
    },

    saveTitleChanges() {
      this.isTitleEditing = false;
      this.title = this.editedTitle.trim();
    },

    cancelTitleChanges() {
      this.isTitleEditing = false;
    },

    toggleDescriptionEdit() {
      this.isDescriptionEditing = true;
      this.editedDescription = this.description;
      this.$nextTick(() => {
        this.$refs.descriptionInput.focus();
      });
    },

    saveDescriptionChanges() {
      this.isDescriptionEditing = false;
      this.description = this.editedDescription.trim();
    },

    cancelDescriptionChanges() {
      this.isDescriptionEditing = false;
    },
  }
};
</script>

<style>
/* Add your style */
</style>
