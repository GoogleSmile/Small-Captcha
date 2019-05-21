<template>
    <div class="captha">
        <input class="input-code" type="text" placeholder="请输入图形验证码" maxlength="4" @blur="bl" v-model="text">
        <img class="imgCaptcha" title="换一张"  src="http://127.0.0.1:3000/img/dianjishuaxin.png" @click="qhyzm" :style="Qstate==false?'display:inline-block':'display:none'">
        <div :style="Qstate==false?'display:none':'display:inline-block'" class="divCaptcha" @click="qhsz">{{div}}</div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            text:'',
            Qstate:false,
            div:''
        }
    },
    methods: {
        bl:function(){
            if(this.text){
            if(this.text==this.div){
                this.$toast("验证码输入正确")
            }else{
                this.$toast("验证码输入不正确,请重新输入");
                this.qhsz()
            }
            }
        },
        qhsz:function(){
            var divText="";
            var list=['0','1','2','3','4','5','6','7','8','9'];
            for(var i=0;i<4;i++){
                var rand=Math.floor(Math.random()*10);
                divText+=rand
            };
            this.div=divText;
        },
        qhyzm:function(){
            this.Qstate=true;
            this.qhsz()
        }
    },
}
</script>
<style scoped>
.input-code {
    padding: 13px 0;
    font-size: 1.6em;
    line-height: normal;
    border: none;
    background-color: #fff;
    color: #333;
    margin-right: 10px;
}
.imgCaptcha {
    width: 92px;
    height: 35px;
}
.divCaptcha {
    width: 92px;
    height: 35px;
    background: #cfcfcf;
    font-size:25px;
    font-style: italic;
    letter-spacing:3px;
    text-align: center;
}
</style>