<script>
  import util from '~/assets/js/util'
  export default {
    async asyncData({ params, $axios }) {
      let discograficas = await $axios.$get('https://api.typewriter.cloud/alicia.bonilla/jazzsite/types/discografica')
      discograficas.forEach(discografica => util.cmsToObj(discografica))
      return {
        discograficas
      }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <h3 style="margin-top: 15px">Discograficas</h3>
   <ul class="ul">
     <li v-for="a of discograficas" :key="a.slug">
       <div class="card">
          <div>
            <img class="card-img" :src="a.image" />
          </div>
          <div class="card-text">
            <h4 class="card-title"><strong> {{ a.name }} </strong></h4>
            <p class="card-description">
              <span>País: {{a.country}}</span><br>
              <span>Fundación: {{a.founded}}</span><br>
            </p>
            <NuxtLink :to="{ name: 'discografica-slug', params: { slug: a.slug } }" class="button">
                Detalles
            </NuxtLink>
          </div>
        </div>
     </li>
   </ul>
   <FooterView />
 </div>
</template>