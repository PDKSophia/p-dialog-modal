<template>
  <div class="modal-mask" @click="handleMaskClose">
    <div class="modal-toastbg">
      <div
        class="modal-content pt-page-scaleBounce"
        :style="{ top: isMarginTop  }"
        @click="handleStopPropagation"
      >
        <div
          class="modal-title"
          :style="{
            backgroundColor: cssStyle.bgTitleColor,
            color: cssStyle.textTitleColor
          }"
        >
          <span>{{ title }}</span>
        </div>
        <div class="content-container" v-if="type === 'normal'">
          {{
          content
          }}
        </div>
        <div class="textarea-container" v-else>
          <textarea
            class="content-box"
            placeholder="输入些啥..."
            v-model="textareaValue"
            :style="{ height: cssStyle.contentHeight }"
          />
        </div>
        <div class="modal-button">
          <div
            class="main-button btn-cancel"
            @click="hangleClickCancel"
            :style="{
              backgroundColor: cssStyle.bgCancelColor,
              color: cssStyle.textCancelColor
            }"
          >{{ cancelText }}</div>
          <div
            class="main-button btn-submit"
            @click="handleClickSubmit"
            :style="{
              backgroundColor: cssStyle.bgSubmitColor,
              color: cssStyle.textSubmitColor
            }"
          >{{ submitText }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ConfirmModal',

  data() {
    return {
      textareaValue: '',
      showToastModal: false
    };
  },
  props: {
    title: {
      type: String,
      default: '弹窗提示您'
    },
    content: {
      type: String,
      default: '你要给我点个赞嘛 ?'
    },
    type: {
      type: String,
      default: 'normal'
    },
    cancelText: {
      type: String,
      default: '取消'
    },
    disableCloseMask: {
      type: Boolean,
      default: true
    },
    submitText: {
      type: String,
      default: '确定'
    },
    cssStyle: {
      type: Object,
      default: function () {
        return {
          bgTitleColor: 'white',
          textTitleColor: '#4a4a4a',
          bgCancelColor: 'white',
          textCancelColor: '#555',
          bgSubmitColor: '#4d4d4d',
          textSubmitColor: '#fff'
        };
      }
    },
    isMarginTop: {
      type: String,
      default: '35%'
    }
  },
  methods: {
    handleMaskClose() {
      if (this.disableCloseMask) {
        console.log('not allowed click close !');
      } else {
        this.$emit('onHandleCancel', false);
      }
    },

    handleStopPropagation(e) {
      e.stopPropagation();
    },
    hangleClickCancel() {
      this.$emit('onHandleCancel', this.type, false)
    },
    handleClickSubmit() {
      if (this.type === 'normal') {
        this.$emit('onHandleOnOk', 'normal', true, '');
      } else {
        this.$emit('onHandleOnOk', 'input', true, this.textareaValue);
      }
    }
  }
};
</script>

<style scoped lang="less">
.modal-mask {
  width: 100%;
  height: 100%;
  opacity: 1;
  position: fixed;
  top: 0px;
  left: 0px;
  z-index: 10;

  .modal-toastbg {
    background-color: rgba(0, 0, 0, 0.4);
    position: absolute;
    width: 100%;
    min-height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;

    .modal-content {
      position: absolute;
      opacity: 1;
      width: 80%;
      background-color: white;
      border-radius: 10px;

      .modal-title {
        font-family: PingFangSC-Semibold;
        font-size: 17px;
        color: #4a4a4a;
        letter-spacing: 1.4px;
        text-align: center;
        padding: 14px 0;
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
      }

      .modal-button {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 42px;
        text-align: center;
        border-top: 2px solid #f1f1f1;

        > .main-button {
          width: 50%;
          padding: 10px;
          font-size: 14px;
          height: 22px;
          line-height: 22px;
          text-align: center;
        }

        > .btn-cancel {
          background-color: #f5f5f5;
          color: #555;
          border-bottom-left-radius: 10px;
        }

        > .btn-submit {
          background-color: #4d4d4d;
          color: #fff;
          border-bottom-right-radius: 10px;
        }
      }
    }
  }
}
.content-container {
  width: 90%;
  padding: 15px 5%;
  line-height: 26px;
  color: #555;
  font-size: 18px;
  text-align: center;
  border-top: 1px solid #f5f5f5;
}
.textarea-container {
  width: 90%;
  padding: 5%;

  > .content-box {
    width: 100%;
    line-height: 22px;
    font-size: 15px;
    height: 110px;
    outline: none;
    padding: 5px;
    box-sizing: border-box;
  }
}
.pt-page-scaleBounce {
  -webkit-animation: scaleBounceLeftIn 0.5s ease-in both;
  -moz-animation: scaleBounceLeftIn 0.5s ease-in both;
  animation: scaleBounceLeftIn 0.5s ease-in both;
}
@-webkit-keyframes scaleBounceLeftIn {
  0% {
    -webkit-transform: scale(0.4);
  }
  25% {
    -webkit-transform: scale(0.7);
  }
  50% {
    -webkit-transform: scale(1.2);
  }
  75% {
    -webkit-transform: scale(0.8);
  }
  100% {
    -webkit-transform: scale(1);
  }
}
@-moz-keyframes scaleBounceLeftIn {
  0% {
    -moz-transform: scale(0.4);
  }
  25% {
    -moz-transform: scale(0.7);
  }
  50% {
    -moz-transform: scale(1.2);
  }
  75% {
    -moz-transform: scale(0.8);
  }
  100% {
    -moz-transform: scale(1);
  }
}
@keyframes scaleBounceLeftIn {
  0% {
    transform: scale(0.4);
  }
  25% {
    transform: scale(0.7);
  }
  50% {
    transform: scale(1.2);
  }
  75% {
    transform: scale(0.8);
  }
  100% {
    transform: scale(1);
  }
}
</style>
