<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const posts = ref([])
const error = ref(null)

onMounted(async () => {
    try {
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts")
        posts.value = response.data
    } catch (err) {
        error.value = "Failed to fetch data."
    }
})
</script>

<template>
    <div>
        <h2>List Posts</h2>
        <p v-if="error">{{ error }}</p>
        <table v-else>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Title</th>
                    <th>Body</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="post in posts" :key="post.id">
                    <td>{{ post.id }}</td>
                    <td>{{ post.title }}</td>
                    <td>{{ post.body }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 16px;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

th, td {
  padding: 12px 16px;
  border-bottom: 1px solid #eee;
  text-align: left;
}

th {
  background: #f5f5f5;
  font-weight: 600;
  color: #333;
}

tr:hover {
  background: #f0f8ff;
}

h2 {
  color: #2c3e50;
  margin-bottom: 8px;
}

p {
  color: #e74c3c;
  font-weight: bold;
}
</style>