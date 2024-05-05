<template>
    <div class="body">
        <div class="login">
        <div>
            <img src="../../assets/img/logo.png" alt="gambar1" width="500px">
        </div>
        <div class="form" >
            <p class="katalogin">Log in</p>
            <table>
                
                <tr>
                   
                    <td><img src="../../assets/img/user.png" alt=""width="25px"></td>
                    <td>:</td>
                    <td><input type="text" placeholder="Username"></td>
                </tr>
                <tr>
                    <td><img src="../../assets/img/lock.png" alt="" width="25px"></td>
                    <td>:</td>
                    <td><input type="text" placeholder="password"></td>
                </tr>
            </table>
            <button>konfirmasi</button>
        </div>
    </div>
    </div>
</template>
<style>
.body{
    background-color: white;
    height: 100vh;
}
.login{
    /* border-style: solid;
    border-color: aqua;
    padding: 10px;
    width: fit-content; */
    display:flex ;
    justify-content: center;
    gap: 50px;
    align-items: center;
    height: 100%;
}

.form{
    background-color: #D8EFE9;
    padding: 20px;
    border-radius: 15px;
}
.katalogin
{
    font-weight: bolder;
    font-size: 64px;
}
input{
    background-color: transparent;
    border: none;
}
td
{
    border-bottom: 2px solid black;
}
button{
    margin: 10px;
    background-color: #252B3B;
    color: white;
    border-radius: 10px;
    padding: 5px 10px;
}
</style>

<script>
export default{
    layout: 'empty',
}
</script>