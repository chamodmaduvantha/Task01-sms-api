<template>
    <div class="container">
        <div class="card text-center">
            <div class="card-header text-left">
                <div class="row">
                    <img src="../assets/sms.png" class="logo">
                    <h4>Send Message</h4>
                </div>
            </div>
            <div class="card-body">
            <form class="form">
                <div class="form-group row mt-3">
                    <label for="inputNumber" class="col-sm-2">Phone Number</label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="inputNumber" v-model="phoneNumber">
                    </div>
                </div>
                <div class="form-group row mt-3">
                    <label for="inputName" class="col-sm-2">Sender Name</label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="inputName" v-model="senderName">
                    </div>
                </div>
                <div class="form-group row mt-3">
                    <label for="inputSms" class="col-sm-2">Message</label>
                    <div class="col-sm-10">
                        <textarea type="text" class="form-control" v-model="message" placeholder="Type send to message......" id="inputSms"></textarea>
                    </div>
                </div>
                <div class="row">
                    <div class="col-6">
                    </div>
                    <div class="col-6  text-right">
                        <button v-on:click="saveData" class="btn">Send Message</button>
                    </div>
                </div>
                
            </form>
            </div>
        </div>
    </div>
</template>



<script>
import axios from 'axios'

export default({
    name:'sendMessage',
    data(){
        return{
            phoneNumber:'',
            senderName:'',
            message:''
        }
    },
    methods:{
        async saveData(){
            console.log("Details",this.phoneNumber,this.senderName,this.message)
            let result = await axios.post("http://localhost:3000/sms",{
                phoneNumber:this.phoneNumber,
                senderName:this.senderName,
                message:this.message
            });
            console.warn(result);
            if(result.status==201){
                alert("Sended Done")
            }
            localStorage.setItem("user-info",JSON.stringify(result.data))
        }
    },
})
</script>


<style>
.form{
    margin-top: 10px;
}
.card-header img{
    height: 100px;
}
.card-header{
    background:url(../assets/bg.jpg) ;
}
.card-header h4{
    margin-top: 50px;
    color: rgb(4, 9, 26);
    font-size: 35px;
}
.card-body{
    text-align: left;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
    background: url(../assets/bgBoady.png);
}
.card-body button{
   background-color: rgb(0, 79, 197);
}
.card{
    margin-top: 100px;
}
</style>