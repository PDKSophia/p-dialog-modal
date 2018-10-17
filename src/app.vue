<template>
  <div class='mask'>
    <div class='toastbg'></div>
      <div class='modal-dialog' :style='[{marginTop: confrimMesasge.marginTop ? confrimMesasge.marginTop : "50%" }]'>
        <div class='modal-title' :style='[{backgroundColor: confrimMesasge.headerColor ? confrimMesasge.headerColor : "#4d4d4d;" }]'>{{ confrimMesasge.title }}</div>
        <div class='modal-input'>
            <p>{{ confrimMesasge.text }}</p>
          </div>
          <div class='modal-button'>
            <div class='main-button btn-cancel'
                @click='handleCancle'
            > {{ confrimMesasge.cancelText }}
            </div>
            <div class='main-button btn-submit'
                :style='[{backgroundColor: confrimMesasge.okColor ? confrimMesasge.okColor : "#4d4d4d;" }]'
                @click='handleOnOk'
            > {{ confrimMesasge.okText }}
            </div>
          </div>
        </div>
      </div>
</template>

<script>
export default {
  props: {
    confrimMesasge: {
      type: Object,
      default: function () {
        return {
          title: 'xxx提示您？',
          text: '我帅吗 ?',
          cancelText: '不帅',
          okText: '帅',
          headerColor: '',
          okColor: '',
          marginTop: '50%'
        }
      }
    }
  },
  methods: {
    handleCancle () {
      console.log('cancle')
      this.$emit('onHandeleCancle', false)
    },
    handleOnOk () {
      console.log('ok')
      this.$emit('onHandeleOnOK', true)
    }
  },
  mounted () {
  }
}
</script>

<style scoped lang='less'>
.mask {
  width: 100%;
  height: 100%;
  opacity: 1;
  position: fixed;
  top: 0px;
  left: 0px;

  > .toastbg {
    opacity: 0.2;
    background-color: black;
    position: absolute;
    width: 100%;
    min-height: 100%;
  }

  > .modal-dialog {
    animation: bounceIn 1s;
    position: absolute;
    opacity: 1;
    width: 70%;
    margin-left: 15%;
    margin-top: 70%;
    background-color: white;

    > .modal-title {
      text-align: center;
      padding: 15px;
      font-size: 15px;
      color: white;
      background-color: #4d4d4d;
    }

    > .modal-input {
      padding: 15px 20px;
      font-size: 16px;
      color: #4d4d4d;
      text-align: center;
    }

    > .modal-button {
      width: 100%;
      display: flex;
      justify-content: center;
      align-content: center;

      > .main-button {
        width: 50%;
        padding: 10px;
        font-size: 13px;
        text-align: center;

        > Button {
          width: 100%;
        }
      }

      > .btn-cancel {
        background-color: #f5f5f5;
        color: #555;
      }

      > .btn-submit {
        background-color:#4d4d4d;
        color: #fff;
      }
    }
  }
}
.placeholder{
  font-size: 15px;
  color: #555;
}
input{
  color: #555 !important;
  font-size: 15px;
  text-align: center;
}
@keyframes bounceIn {
  from,
  20%,
  40%,
  60%,
  80%,
  to {
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }

  0% {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }

  20% {
    transform: scale3d(1.1, 1.1, 1.1);
  }

  40% {
    transform: scale3d(0.9, 0.9, 0.9);
  }

  60% {
    opacity: 1;
    transform: scale3d(1.03, 1.03, 1.03);
  }

  80% {
    transform: scale3d(0.97, 0.97, 0.97);
  }

  to {
    opacity: 1;
    transform: scale3d(1, 1, 1);
  }
}
</style>
