<template>
  <!--begin::Aside-->
  <div class="info-box">
    <div class="row mt-5">
        <Voltar route="/" />
      <div class="col-xl-12">
        <div class="d-flex flex-column-fluid row">
          <div class="col-md-8 col-12 ">
            <Plans image="media/site-images/Unauthorized" />
          </div>
          <div class="col-md-4 col-12">
            <Depositions />
          </div>
        </div>
      </div>
    </div>
    <Pro>
      <div class="card card-custom Authorized p-7 mt-3">
                              <h2>OPS, Pagamento não autorizado!</h2>
                                    <div class="mt-20 receipt">
                                    <img src="@/assets/media/site-images/Uauth-receipt.png">
                                    </div>
                                    
                                    <span class="receipttxt"><p>O seu pagamento foi confirmado, agora você já pode iniciar as suas automações, escolha os robôs que irão te ajudar em seus projeto.</p></span>
                                    <div class="verRobos">
                                    <a href="#" class="btn btn-white font-weight-bold btn-square mt-20">VER ROBÔS</a>
                                    </div>
                        
                           </div>
    </Pro>

    <!--begin::Dashboard-->
    <!--end::Dashboard-->
  </div>
  <!--end::Container-->
</template>

<script>
import Depositions from "@/common/components/Depositions";
import Pro from "@/common/components/Pro";
import Plans from "@/common/components/Plans";
import Voltar from "@/common/components/layout/Voltar";

export default {
  components: {
    Depositions,
    Pro,
    Plans,
    Voltar
  },
};
</script>

<style></style>
