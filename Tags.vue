<template>
  <div>
    <b-row>
      <b-col cols="12" class="label">
        <b-form-group label="Tags" label-for="tags">
          <b-input-group>
            <b-input-group-prepend>
              <b-input-group-text class="bg-light">
                <b>
                  <b-icon icon="tag"></b-icon>
                </b>
              </b-input-group-text>
            </b-input-group-prepend>
            <b-form-input
              id="tags"
              class="border-right-0"
              placeholder="Add a tag"
              v-model="addingTag"
              @keydown.enter="appendTag(addingTag)"
              @blur="appendTag(addingTag)"
            ></b-form-input>
          </b-input-group>
        </b-form-group>
      </b-col>

      <b-col cols="12" v-if="tags.length > 0">
        <div class="tag-container">
          <template v-for="(tag, index) in tags">
            <div :key="index" class="tag bg-light">
              {{ tag }}
              <span class="delete-icon" @click="removeTag(index)">
                <b-icon icon="x"></b-icon>
              </span>
            </div>
          </template>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Tags",
  data() {
    return {
      addingTag: "",
      tags: [],
    };
  },
  methods: {
    appendTag(tag) {
      if (this.tags.includes(tag)) {
        return;
      }
      if (tag === "") {
        return;
      }
      this.tags.push(tag);
      this.addingTag = "";
    },

    removeTag(index) {
      this.tags.splice(index, 1);
    },
  },
};
</script>

<style>
.tag {
  white-space: nowrap;
  padding: 6px 12px;
  border-radius: 5px;
  margin-right: 10px;
  margin-bottom: 10px;
}

.tag-container {
  display: flex;
  flex-wrap: wrap;
}

.delete-icon {
  color: #051d40;
}

.delete-icon:hover {
  color: #4fc0e8;
}
</style>
