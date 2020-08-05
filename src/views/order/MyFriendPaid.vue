<template>
  <div class="return-list" ref="container">
    <div id="qrCode" ref="qrCodeDiv"></div>
    <Loading :loaded="loaded" :loading="loading"></Loading>
  </div>
</template>

<script>
import QRCode from 'qrcodejs2';
import Loading from "@components/Loading";

export default {
  name: "ReturnList",
  components: {
    Loading
  },
  data() {
    return {
      orderList: [],
      page: 1,
      limit: 20,
      loading: false,
      loaded: false
    };
  },
  methods: {
    // getOrderList() {
    //   const { page, limit } = this;
    //   if (this.loading || this.loaded) return;
    //   this.loading = true;
    //   getOrderList({
    //     page,
    //     limit,
    //     type: -3
    //   }).then(res => {
    //     this.orderList = this.orderList.concat(res.data);
    //     this.loading = false;
    //     this.loaded = res.data.length < limit;
    //     this.page++;
    //   });
    // }
  },
  mounted() {
    new QRCode(this.$refs.qrCodeDiv, {
        text: "https://www.baidu.com",
        width: 100,
        height: 100,
        colorDark: "#333333", //二维码颜色
        colorLight: "#ffffff", //二维码背景色
        correctLevel: QRCode.CorrectLevel.L //容错率，L/M/H
    });
  }
};
</script>

<style scoped>
    .return-list{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
    }
    #qrCode{
        position: fixed;
        bottom: 20%;
    }
</style>
