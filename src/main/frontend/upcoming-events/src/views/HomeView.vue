<script setup>
import { RouterLink } from "vue-router"

import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";
import CardsRecomendados from "../components/CardsRecomendados.vue";
import CardsEvents from "../components/CardsEvents.vue";
import CloseSession from "../components/CloseSession.vue";
import { useEventsStore } from "../stores/Events";
import { onBeforeMount } from "vue";

const store = useEventsStore();
onBeforeMount(async () => {
  await store.fetchEvents();
});
</script>

<template>
  <Header></Header>
  <div id="RecomendadosContainer">
    <div id="TitleAndButton">
    <h2>Nuestros recomendados:</h2>
    <div id="ContainerButton"><CloseSession></CloseSession></div></div>
    <div class="eventosRecomendados">
      <CardsRecomendados v-for="event in store.EventsRecommended" :event="event"></CardsRecomendados>
    </div>
  </div>

  <div id="EventsContainer">
    <h2>Todo lo que puedes ver y hacer:</h2>
    <div class="eventos">
      <CardsEvents v-for=" event in store.Events" :event="event"></CardsEvents>
    </div>
  </div>
  <Footer></Footer>
</template>

<style lang="scss" scoped>
@import "../assets/scss/Variables.scss";

* {
  font-family: Dosis;
  #TitleAndButton{
    display: flex;
    justify-content: space-between;
    margin-top: 2vw;
  #ContainerButton{
    display: flex;
    justify-content: flex-end;
    margin-right: 24vh;
    margin-bottom: 3vh
  }}

  h2 {
    color: $Blue;
    
    margin-top: 40px;
    margin-left: 8%;
    
    font-weight: 700;
    
  }

  .eventosRecomendados {
    padding: 0 40px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 20px;
  }

  .eventos {
    padding: 0 40px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  @media (max-width:1200px) {
    .eventosRecomendados {
      grid-template-columns: 1fr 1fr 1fr;
    }
    footer{
      display: none;
    }
  }
  @media (max-width:1000px) {
    .eventosRecomendados {
      grid-template-columns: 1fr 1fr;
    }
    .eventos {
      grid-template-columns: 1fr;
    }
    footer{
      display: none;
    }
  }


  @media (max-width:700px) {
    .eventosRecomendados {
      grid-template-columns: 1fr;
    }
    footer{
      display: none;
    }
  }
}

</style>
