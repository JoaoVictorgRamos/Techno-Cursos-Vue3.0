<template>
  <div>
    <div v-if="loading">
      <PageLoading />
    </div>
    <transition>
      <div v-if="api" class="conteudo">
        <div>
          <h1>{{ api.nome }}</h1>
          <p>{{ api.descricao }}</p>
          <h2>Aulas</h2>
          <ul class="aulas">
            <li v-for="MyAula in api.aulas" :key="MyAula.id">
              <router-link
                :to="{
                  name: 'MyAula',
                  params: { MyAula: MyAula.id },
                }"
                >{{ MyAula.nome }}</router-link
              >
            </li>
          </ul>
        </div>
        <router-view></router-view>
      </div>
    </transition>
  </div>
</template>

<script>
import fetchData from "@/mixins/fetchData.js";
import PageLoading from "@/components/PageLoading.vue";
export default {
  components: { PageLoading },
  name: "MyCurso",
  props: ["MyCurso"],
  mixins: [fetchData],
  created() {
    this.fetchData(`/curso/${this.MyCurso}`);
  },
};
</script>

<style>
.aulas {
  display: flex;
  flex-direction: column;
}
.aulas li a {
  display: block;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  background: white;
  padding: 20px;
  margin-bottom: 10px;
  border-radius: 4px;
}

.aulas li a.router-link-active {
  background: #4b8;
  color: white;
}
</style>
