<template>
  <div class="button-cep">
    <img src="../assets/plus.png" alt=""><p class="text-button">{{textButton}}</p>
  </div>
</template>

<script>
export default {
  name: 'ButtonCep',
  props: {
    textButton: String
  }
}
</script>

<style>
.button-cep{
margin: 0;
display: flex;
flex-direction: row;
justify-content: center;
align-items: center;
padding: 16px 211px;
gap: 10px;
position: absolute;
width: 0px;
height: 20px;
left: 460px;
top: 121px;
background: #B600EE;
border-radius: 8px;
padding-left: 140px;
padding-right: 140px;
cursor: pointer;
}
.text-button{
padding-left: 10px;
height: 22px;
font-family: 'Open Sans';
font-style: normal;
font-weight: 700;
font-size: 16px;
line-height: 22px;
display: flex;
align-items: center;
color: #FFFFFF;
flex: none;
order: 1;
flex-grow: 0;
}
</style>