<template>
  <div>
    <h1>Upload PDF File</h1>
    <label :for="name" class="cursor-pointer border bg-slate-600 p-4">
      halo
      <input
        :id="name"
        :name="name"
        type="file"
        multiple
        accept=".pdf"
        :v-model="file"
        @change="fileUpload"
        class="hidden"
      />
    </label>

    <div>
        <span>
            {{ file?.name }}
        </span>
    </div>
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

// console.log(file.value);
// async function uploadPdfFile(event) {
//   await event.target.click();
//   const file = event.target.file;

//   const formData = new FormData();
//   formData.append("file", file);
//   handleChange(file.value);
// }

const fileUpload = async (event) => {
  // event.preventDefault();
  console.log(event.target.files[0]);
  console.log(event.target.files[0].name);
  console.log(event.target.files[0].size/1024);

  const data = {
    name: event.target.files[0].name,
    size: event.target.files[0].size / 1024,
  }
  file.value = data
  files.value.push(data)
//   if (!event.target.file) {
//     return;
//   }
//   const file = event.target.files[0];

  const formData = new FormData();
  formData.append("file", file);
  // const res = await axios.post("http://localhost:3000/upload", formData);
  // console.log(res.data);
};
console.log(files.value);

definePageMeta({
  layout: "",
});
</script>
