<template>
  <!--begin::Aside-->
  <div class="info-box">
    <div class="row mt-5">
        <Voltar route="/" />
      <div class="col-xl-12">
        <div class="d-flex flex-column-fluid row">
          <div class="col-md-8 col-12 ">
            <Plans image="media/site-images/pricing" />
          </div>
          <div class="col-md-4 col-12">
            <Depositions />
          </div>
        </div>
      </div>
    </div>
    <div class="row mt-3">
      <div class="col-xl-12">
        <div class="d-flex flex-column-fluid row" v-if="!emptyPlansCard">
          <PricePlanCard
            v-for="plan in plans"
            :key="plan.id"
            :id="plan.id"
            :title="plan.title"
            :description="plan.description"
            :value="plan.value"
            :max_usage="plan.max_usage"
            :max_bots="plan.max_bots"
            :active="plan.active"
          />
        </div>
        <div class="col-md-12 col-12" v-else>
          <!-- No plans available -->
        </div>
      </div>
    </div>

    <!--begin::Dashboard-->
    <!--end::Dashboard-->
  </div>
  <!--end::Container-->
</template>

<script>
import axios from 'axios';
import Depositions from "@/common/components/Depositions";
import Pro from "@/common/components/Pro";
import Plans from "@/common/components/Plans";
import PricePlanCard from '@/common/components/PricePlanCard';
import Voltar from "@/common/components/layout/Voltar";

export default {
  components: {
    Depositions,
    Pro,
    Plans,
    PricePlanCard,
    Voltar
  },
  data() {
    return {
      plans: []
    }
  },
  methods: {
    async getPlans(){
      try {
        const endpoint = '/plans';

        const response = await axios.get(endpoint)

        const results = response.data
        this.plans = results
        // .filter(plan => plan.layout_active == 1)
        .map(plan => ({
          id: plan.id,
          title: plan.title,
          description: plan.description,
          value: plan.value,
          max_usage: plan.max_usage,
          max_bots: plan.max_bots,
          active: false,
        }))
      } catch(err){
        if(err.response)
          console.log("Server error: " + err);
        else if(err.request)
          console.log("Network error: "+ err);
        else
          console.log("Client error: "+ err);
      }
    }
  },
  created() {
    this.getPlans()
  },
  computed: {
    emptyPlansCard(){
      return this.plans.length == 0
    },
  }

};
</script>

<style></style>
