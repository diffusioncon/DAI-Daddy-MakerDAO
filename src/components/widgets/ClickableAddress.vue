<template>
  <div v-if="ethAddress">
    <a class="eth-address" :href="buildLink" target="_blank" style="color: white;">
      <span>
        <a-row type="flex">
          <a-col :span="5">
            <jazzicon :address="ethAddress" :diameter="25"></jazzicon>
          </a-col>

          <a-col :span="12" style="padding-top:3px;padding-left:5px;margin-right:25px">{{ dotDotDot }}</a-col>
        </a-row>
      </span>
    </a>
  </div>
</template>

<script>
/* global web3:true */
import { mapGetters, mapState } from "vuex";

export default {
  name: "clickableAddress",
  components: {},
  props: {
    ethAddress: {
      type: String
    }
  },
  computed: {
    ...mapState(["etherscanBase"]),
    dotDotDot: function() {
      if (this.ethAddress) {
        return (
          this.ethAddress.substr(0, 6) +
          "..." +
          this.ethAddress.substr(
            this.ethAddress.length - 6,
            this.ethAddress.length
          )
        );
      }
      return "";
    },
    buildLink: function() {
      return `${this.etherscanBase}/address/${this.ethAddress}`;
    }
  }
};
</script>

 <style lang="scss" scoped>
// // Eth Address
.eth-address {
  display: inline-block;
  padding-top:7px;
  padding-left:7px;
  padding-bottom:3px;
  border-radius: 20px;
  background: rgba(#ffcae5, 0.5);
}
</style>
