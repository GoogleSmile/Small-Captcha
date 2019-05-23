<!--基于Vue_cli的图形验证码组件(不区分大小写)-->
<template>
    <div class="captha">
        <!--输入文本框-->
        <input class="input-code" type="text" placeholder="请输入图形验证码" maxlength="4" @blur="bl" v-model="content">
        <!--蒙版-->
        <img class="imgCaptcha" title="换一张"  src="http://127.0.0.1:3000/img/dianjishuaxin.png" @click="changeSwitch" :style="Qstate==false?'display:inline-block':'display:none'">
        <!--验证码-->
        <div :style="Qstate==false?'display:none':'display:inline-block'" class="divCaptcha" @click="changeRandom">{{randomCode}}</div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            content:'', //文本框输入内容
            Qstate:false, //用来控制蒙版显示隐藏
            randomCode:''  //验证码
        }
    },
    methods: {
        bl:function(){      //input的失焦事件
            if(this.content){  //如果有内容，判断input内容与随机码是否一样
            if((this.content).toLowerCase()==this.randomCode){   //如果一样则提示输入正确
                this.$toast("验证码输入正确") 
            }else{                              //如果不一样 则刷新验证码，提示重新输入
                this.$toast("验证码输入不正确,请重新输入");  
                this.changeRandom()
            }
            }
        },
        changeRandom:function(){   //点击生成随机验证码赋到div
            var divText="";
            var list=[0,1,2,3,4,5,6,7,8,9,'a','b','c','d','e','f','g'];
            for(var i=0;i<4;i++){
                var rand=Math.floor(Math.random()*list.length);
                divText+=list[rand]
            };
            this.randomCode=divText;
        },
        changeSwitch:function(){   //点击蒙版显示图形验证码
            this.Qstate=true;
            this.changeRandom()
        }
    },
}
</script>
<style scoped>
.captha{
    display:flex
}
.input-code {
    padding: 13px 0;
    font-size: 16px;
    border: none;
    background-color: #fff;
    color: #333;
    margin-right: 10px;
    width:300px;
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
    padding:7px;
}
</style>