<template>
    <div class="wrapper-popup">
        <div class="rule">
            <h3>Rules</h3>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Incidunt deserunt distinctio fuga, eligendi reiciendis eos. Sunt, provident reprehenderit ipsam quam expedita voluptatibus porro quisquam facilis cumque? Natus, voluptate. Aliquam, provident.</p>
            <button class="confirm">Agree</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "PopupRule",
    data: function(){
        return {
            
        }
    }
    
}
</script>

<style scoped>
.wrapper-popup{
    position: fixed;
    top:0;
    left:0;
    right:0;
    bottom: 0;
    background-color: rgb(0, 0, 0, 0.4);
}

.rule{
    width: 400px;
    top: 40%;
    left:35%;
    padding: 2%;
    background-color: aliceblue;
    position: absolute;
}

.rule .confirm{
    cursor: pointer;
    margin-top: 5px;
    padding:8px 15px;
    border: 2px solid rebeccapurple;
    background-color: beige;
   -webkit-transition: width 2s; /* For Safari 3.1 to 6.0 */
    transition: ease  0.5s;
}


.rule .confirm:hover{
   font-weight: 600;
   color: #fff;
    background-color: rgb(60, 50, 197);
    border: 2px solid#fff;
}

</style>