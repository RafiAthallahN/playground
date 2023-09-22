<template>
  <div>
    <h1>Upload PDF Files</h1>

    <div v-for="(file, index) in files" :key="index">
      <span>{{ file.name }}</span>
      <span>{{ file.size }}</span>
    </div>

    <label :for="name" class="cursor-pointer border bg-slate-600 p-4">
      Upload Files
      <input
        :id="name"
        :name="name"
        type="file"
        multiple
        accept=".pdf"
        :v-model="file"
        @change="fileUpload(index)"
        class="hidden"
      />
    </label>
  </div>
</template>

<script setup>
import axios from "axios";
import { useField } from "vee-validate";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const name = toRef(props, "name");
const { handleChange } = useField(name);

const file = ref(null);
const files = ref([]);

    // console.log(files.value);
const fileUpload = async (event, index) => {
  const file = event.target.files[0];

  const formData = new FormData();
  formData.append("file", file);

  // Upload the file to your server.
  // const res = await axios.post("http://localhost:3000/upload", formData);
  // console.log(res.data);

  // Update the files array.
  files.value[index] = {
    name: file.name,
    size: file.size / 1024,
  };
};

definePageMeta({
  layout: "default",
});
</script>
