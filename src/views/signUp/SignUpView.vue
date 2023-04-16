
<template>
    <div class="box">
        <div class="register">
            <h1>欢迎注册FIM</h1>
            <div class="content">
                <p>每一天，乐在沟通</p>
            </div>
            <div class="select1">
                <form action="">
                    <input type="text" placeholder="昵称" v-model="user.username">
                    <input type="password" placeholder="密码" v-model="user.userPassword">
                    <input type="email" placeholder="邮箱" v-model="user.userEmail">
                    <select name="" id="">
                        <option value="中国 +86">+86</option>
                    </select>
                    <input type="tel" class="phone_number" placeholder="手机号码" v-model="user.userPhone">
                    <input type="button" class="get_code" value="获取" @click="getCode">
                    <input type="text" placeholder="验证码" v-model="user.code">
                </form>
            </div>
            <div class="enter">
                <input type="submit" @click="submit" value="立即注册">
            </div>
            <div class="agree">
                <input type="checkbox" v-model="check">
                我已阅读并同意相关服务条款和隐私政策
            </div>
            <div class="footer">
                <p>Copyright @ 2022-2023 FIM All Rights Reserved</p>
            </div>
        </div>
    </div>
</template>

<script lang="js">
import axios from 'axios'

export default {
    data() {
        return {
            user: {
                username: '',
                userPassword: '',
                userEmail: '',
                userPhone: '',
                code: ''
            },
            check: false,
        }
    },
    methods: {
        submit() {

            if (this.check === false) {
                alert('请先阅读服务条款和隐私政策')
            } else {
                const axios = require('axios')
                const request = axios.create()
                request.post('http://localhost:4444/api/signup/' + this.user.code, this.user).then((res) => {
                    let data = res.data
                    if (data.code === 0) {
                        alert("注册成功")
                        this.user = {
                            username: '',
                            userPassword: '',
                            userEmail: '',
                            userPhone: '',
                            code: ''
                        }
                        this.check = false
                    } else {
                        alert(data.msg)
                    }
                })
            }
        },
        getCode() {
            const request = axios.create()
            request.get('http://localhost:4444/api/getCode/' + this.user.userPhone).then((res) => {
                let data = res.data;
                if(data.code === 0) {
                    alert('验证码已发送')
                }
            })
        }
    }
}

</script>


<style>
* {
    margin: 0px;
    padding: 0px;
}

body {
    background-color: rgb(231, 226, 226);
}

.box {
    margin: 100px auto;
    width: 880px;
    height: 960px;
    background-color: #ffffff;
}

.nav {
    height: 80px;
    font-size: 17px;
    /* background-color: rgb(209, 239, 248); */
}

.nav img {
    float: left;
    width: 630px;
    height: 80px;
}

.nav form .font {
    float: left;
    height: 80px;
    width: 100px;
    border: none;
    font-size: 17px;
    color: #666666
        /* background-color: rgb(126, 89, 89); */
}

.nav p a {
    display: inline-block;
    margin-left: 30px;
    line-height: 80px;
    text-decoration: none;
    color: #666666;
}

.nav p a:hover,
.nav form .font:hover {
    color: #000000;
}

.register {
    margin: 0px 180.5px;
    width: 515px;
    height: 750px;
    background-color: #fff;
}

.register h1 {
    margin-left: 15px;
    height: 100px;
    font-size: 45px;
    line-height: 100px;
    font-weight: 400;
    /* background-color: rgb(230, 150, 150); */
}

.register .content {
    margin: 0px 15px;
    height: 70px;
    text-align: center;
    font-size: 30px;
    /* background-color: rgb(94, 240, 196); */
}

/* .register .content p {
    float: left;
} */

.register .content a {
    float: right;
    text-decoration: none;
    color: rgb(97, 171, 255);
}

.register div[class^="select"] {
    height: 525px;
}

.register div input {
    margin: 28px 15px;
    height: 50px;
    width: 480px;
    border: 0.8px solid rgb(179, 179, 179);
    border-radius: 5px;

    font-size: 20px;
    text-indent: 20px;
    color: rgb(179, 179, 179);
}

.register div select {
    float: left;
    margin: 28px 15px 5px;
    height: 50px;
    width: 100px;
    border: 0.8px solid rgb(179, 179, 179);
    border-radius: 5px;

    font-size: 20px;
    text-indent: 20px;
    /* color: rgb(179, 179, 179); */
}

.register div .phone_number {
    float: left;
    margin: 28px 5px 15px;
    height: 50px;
    width: 250px;
    border: 0.8px solid rgb(179, 179, 179);
    border-radius: 5px;

    font-size: 20px;
    text-indent: 20px;
    /* color: rgb(179, 179, 179); */
}

.register div .get_code {
    float: right;
    margin-left: 0px;
    width: 90px;
    background-color: #3588ff;
    color: white;
}

.register div input:hover,
select:hover {
    border-color: rgb(119, 119, 119);
}

.register div input:focus,
select:focus {

    border: 0.8px solid #549df8;
    /*由于border较细，将outline设置为none。视觉上体验更佳！😂*/
    outline: none;
}

/* .register div:nth-of-type(2n) {
            background-color: rgb(231, 207, 207);
        } */

.register .enter {
    height: 135px;
}

.register .enter input {
    height: 60px;
    font-size: 23px;
    color: #ffffff;
    font-weight: 200;
    background-color: #3588ff;
}

.register .enter input:hover {
    background-color: #327eeb;
}

.register .agree {
    height: 25px;
    font-size: 15px;
    color: rgb(179, 179, 179);
    line-height: 25px;
    /* background-color: rgb(193, 240, 252); */
}

.register .agree input {
    margin: 0px 0px 0px 15px;
    height: 17px;
    width: 17px;
    /* color: #3588ff;
            background-color: #fff; */
}

.register .rule {
    height: 75px;
    /* background-color: rgb(245, 149, 240); */
}

.register .footer {
    height: 32px;
    color: rgb(194, 192, 192);
    text-align: center;
    font-size: 13px;
    line-height: 32px;
}
</style>