<template>
  <li class="nav-item dropdown">
    <a class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
      {{ $t("verification") }}
    </a>
    <div class="dropdown-menu" aria-labelledby="navbarDropdown">
      <a @click="test()" class="dropdown-item">Test sending the model</a>
      <a v-for="item in menu_options" v-bind:key="item.label" v-on:click="clear_overlays(); item.func(current_graph, cell_errors, cell_overlays);" class="dropdown-item">
        {{ item.label }}
      </a>
      <a @click="clear_overlays()" class="dropdown-item">Clear errors</a>
    </div>
  </li>
</template>

<script>
import axios from "axios";
import { setupModal, modalH3, modalSimpleText } from '../../assets/js/common/util'

export default {
  data: function(){
    return {
      model_data:"", //stores the mxgraph model data
      errors:[], //errors
      modelType:"", //stores the model type (feature, component, etc)
      menu_options: [], //stores the custom verification menu options
      current_verification:"", //stores the current verification function
      cell_errors:[], //stores the cells that contains errors
      cell_overlays:[] //stores the overlays that show errors
    }
  },
  props: {
   current_graph: {
    type: Object,
    required: true
   }
  },
  mounted: function(){
    this.initialSetup();
  },
  watch:{
    $route (to, from){
      if(this.$route.name === 'Models')
      {
        this.initialSetup();
      }
    }
  },
  methods: {
    // executes an initial setup in which the custom model verification file is loaded
    initialSetup(){
      this.modelType=this.$route.params.type;
      this.menu_options=[];
      try {
        //load custom model verification file
        var verificationToImport = require('@/assets/js/models/custom/verification/'+this.modelType+'.js');
        this.currentVerification = verificationToImport.default();
        this.menu_options=this.currentVerification;
      } catch (ex) {
        //no verification available - nothing to do
      }
    },
    //clear all the overlays
    clear_overlays(){
      for (var i = 0; i < this.cell_errors.length; i++) {
        this.current_graph.removeCellOverlay(this.cell_errors[i], this.cell_overlays[i]);
      }
      this.cell_errors=[];
      this.cell_overlays=[];
    },
    //executes a test sending the current mxgraph model to the backend server
    test(){
      if (localStorage["domain_implementation_main_path"]) {
        this.errors=[];
        var encoder = new mxCodec();
        var result = encoder.encode(this.current_graph.getModel());
        var xml = mxUtils.getXml(result);
        axios.post(localStorage["domain_implementation_main_path"]+'Verification/test', {
          data: xml
        })
        .then(response => {
          var c_header = modalH3("Test response");
          var c_body = modalSimpleText(response.data);
          setupModal(c_header,c_body);
        })
        .catch(e => {
          this.errors.push(e); 
          var c_header = modalH3(this.$t("modal_error"),"error");
          var c_body = modalSimpleText(e + this.$t("model_actions_backend_problem"));
          setupModal(c_header,c_body);
        });
      }else{
        var c_header = modalH3(this.$t("modal_error"),"error");
        var c_body = modalSimpleText(this.$t("verification_path_problem"));
        setupModal(c_header,c_body);
      }
      
    }
  }
}
</script>

<style scoped>
</style>