<template>
  <!-- Component de card -->
  <div class="col-sm-3">
    <div class="card card-custom Pricing Pricing-card_6 p-7">
      <div class="Pricing-card_3_grp-1 h-100">
        <h3>{{ title }}</h3>
        <p>
          {{ description }} <br>
          Pensando em você que precisa ter um consumo
          alto de automação e vários projetos ao mesmo tempo
        </p>
        <span class="R$">{{ value }} / mês</span>

        <div class="btn15off mt-2" v-if="discount">
          <button type="button" class="btn btn-primary btn-sm p-3 mb-2">
            10% OFF
          </button>
          <p>
            Neste plano você ativa descontos em cada um dos robôs, a
            porcentagem acima se aplica em cada requisição.
          </p>
        </div>
      </div>
      <div class="Pricing-card_3_grp-2">
        <span>Recursos deste plano</span>
        <div class="d-flex pt-5">
          <div class="symbol-img mr-5 icn_history">
            <span class="symbol"
              ><img src="@/assets/media/site-images/icn_history1.png"
            /></span>
          </div>
          <div class="d-flex align-items-center">
            <span class="font-weight-bold" v-if="max_usage >=0"
              >Até {{ max_usage }} requisições</span
            >
            <span class="font-weight-bold" v-else>
              Requisições Ilimitadas
            </span>
          </div>
        </div>
        <div class="d-flex">
          <div class="symbol-img mr-5 icn_history">
            <span class="symbol"
              ><img src="@/assets/media/site-images/icn_my-services1.png"
            /></span>
          </div>
          <div class="d-flex align-items-center">
            <span class="font-weight-bold" v-if="max_bots >=0"
              >Até {{ max_bots }} robôs ativos</span
            >
            <span class="font-weight-bold" v-else>
              Robôs Ilimitados
            </span>
          </div>
        </div>

        <p class="mt-10">
          <i class="fa fa-check mr-2" aria-hidden="true"></i>Dashboard de
          Consumo
        </p>
        <p>
          <i class="fa fa-check mr-2" aria-hidden="true"></i>Resumo de
          Consumo
        </p>
      </div>
      <div class="btn_COMPRAR">
        <button class="btn btn-orange mt-3">COMPRAR CRÉDITOS</button>
      </div>
    </div>
  </div>
  <!-- End Component -->
</template>

<script>
export default {
  props: {
        id: {
            type: Number,
            required: true
        },
        title: {
            type: String,
            required: true
        },
        description: {
            type: String,
            required: true
        },
        discount: {
            type: String,
            required: false
        },
        value: {
            type: String,
            required: true
        },
        max_usage: {
            type: Number,
            required: true
        },
        max_bots: {
            type: Number,
            required: true
        },
        active: {
            type: Boolean,
            required: true
        }
    }
};
</script>

<style>
</style>