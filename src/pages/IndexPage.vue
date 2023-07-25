<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        title="Harry Potter"
        :rows="posts"
        :columns="columns"
        row-key="name"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import { api } from "boot/axios";

export default defineComponent({
  name: "IndexPage",
  setup() {
    const posts = ref([]);
    const columns = [
      {
        name: "name",
        field: "name",
        label: "Nome",
        sortable: true,
        align: "left",
      },
      {
        name: "house",
        field: "house",
        label: "Casa",
        sortable: true,
        align: "left",
      },
      {
        name: "actor",
        field: "actor",
        label: "Ator",
        sortable: true,
        align: "left",
      },
      {
        name: "gender",
        field: "gender",
        label: "Gênero",
        sortable: true,
        align: "left",
      },
      {
        name: "species",
        field: "species",
        label: "Raça",
        sortable: true,
        align: "left",
      },
      {
        name: "patronus",
        field: "patronus",
        label: "Patrono",
        sortable: true,
        align: "left",
      },
      {
        name: "image",
        field: "image",
        label: "Foto",
        sortable: true,
        align: "left",
      },
    ];

    onMounted(() => {
      getPosts();
    });

    const getPosts = async () => {
      try {
        const { data } = await api.get("characters");
        posts.value = data;
        console.log(data);
      } catch (error) {
        console.error(error);
      }
    };

    return {
      posts,
      columns,
    };
  },
});
</script>
