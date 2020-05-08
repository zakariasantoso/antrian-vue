<template>
  <div class="container-antrian-page">
    <div class="container">
      <div class="row">
        <div class="antrian">{{noAntrian}}</div>
        <div class="iklan-kanan">
          <video src="../assets/example.mp4" autoplay muted loop></video>
        </div>
      </div>
      <div class="row-bawah">
        <div class="iklan-bawah">
          <video src="../assets/example.mp4" autoplay muted loop></video>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => {
    return {
      noAntrian: null
    };
  },
  mounted() {
    this.getNoAntrian();
  },
  methods: {
    getNoAntrian() {
      setInterval(() => {
        axios
          .get("http://localhost/antrian/api")
          .then(resp => {
            this.noAntrian = resp.data.data.no_antrian;
          })
          .catch(err => {
            console.log("request failed!", err);
          })
          .finally(() => {});
      }, 1000);
    }
  }
};
</script>

<style lang="scss">
.container-antrian-page {
  display: flex;
  justify-content: center;
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 80%;

    input {
      margin: 10px;
    }

    .row {
      display: flex;
      justify-content: space-evenly;
      max-width: 100vw;

      .antrian {
        min-width: 300px;
        min-height: 300px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgb(116, 116, 116);
        font-size: 60px;
        margin: 7px;
      }

      .iklan-kanan {
        video {
          height: 300px;
          margin: 7px;
        }
      }
    }
    .row-bawah {
      width: 100%;
      .iklan-bawah {
        width: 100%;
        video {
          width: 100%;
        }
      }
    }
  }
}
</style>