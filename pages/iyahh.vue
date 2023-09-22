<template>
  <div>
    <h1>File Upload</h1>
    <form>
      <label for="file">File: </label>
      <input type="file" name="file" @change="onChange" />
    </form>
  </div>

  <div>
    <span>
        {{  }}
    </span>
  </div>
</template>
<script setup>

const files = ref([])
const onChange = async (e) => {
  const files = e.target.files;
  
  const formData = new FormData();
  formData.append('file', files[0]);
  await useFetch('/api/upload', {
    method: 'post',
    body: formData,
  });
  files.value.push(files)
  console.log(files[0].name);
};

definePageMeta({
    layout: ''
})
</script>