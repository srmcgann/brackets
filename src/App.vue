<template>
  <BracketsGame/>
</template>

<script>
import BracketsGame from './components/BracketsGame'

export default {
  name: 'App',
  components: {
    BracketsGame
  }
}
</script>

<style>
html{
  margin:0;
  height: 100%;
  overflow: hidden;
}
body{
  margin: 0;
  height: 100%;
  background-size: 100vw 100vh;
  background-image: linear-gradient(#234, #000);
  color: #ffa;
  overflow: hidden;
}
input{
  cursor: pointer;
}
input:focus, textarea:focus, select:focus {
  outline: none;
}
.main{
  margin-top: 25px;
  font-family: arial, tahoma;
  width: 100%;
  text-align: center;
}
.header{
  width: 100%;
  text-align: right;
}
.headerControls{
  margin-right: 40px;
  font-size: 24px;
}
.logo{
  width: 60px;
  position: absolute;
}
.siteLogo{
  position: absolute;
  width: 200px;
  margin-top: -20px;
  margin-left: -15px;
  left: 10px;
}
.tableContainer {
  display: flex;
  justify-content: center;
}
table{
  border-collapse: collapse;
}
input[type=checkbox]{
  transform: scale(2.0);
}
td{
  height: 80px;
  min-width: 90px;
  width: 5vw;
  position: relative;
}
.intermediaryTD{
  border-bottom: 3px solid #2fa;
}
.topLeft:after{
  content: "";
  background: #2fa;
  position: absolute;
  bottom: 0;
  right: 0;
  height: 50%;
  width: 3px;
}
.bottomLeft:after{
  content: "";
  background: #2fa;
  position: absolute;
  top: 0;
  right: 0;
  height: 50%;
  width: 3px;
}
.topRight:after{
  content: "";
  background: #2fa;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 50%;
  width: 3px;
}
.bottomRight:after{
  content: "";
  background: #2fa;
  position: absolute;
  top: 0;
  left: 0;
  height: 50%;
  width: 3px;
}
h1 {
 overflow: hidden;
 text-align: left;
 font-size: 16px;
}
h1:after {
 background-color: #2fa;
 content: "";
 display: inline-block;
 height: 3px;
 position: relative;
 vertical-align: middle;
 width: 100%;
 left: 50%;
 margin-right: -50%;
}
h2 {
 overflow: hidden;
 text-align: right;
 font-size: 16px;
}
h2:after {
 background-color: #2fa;
 content: "";
 display: inline-block;
 height: 3px;
 position: relative;
 vertical-align: middle;
 width: 100%;
 right: 50%;
 margin-left: -50%;
}
hr{
  height: 0;
  margin:0;
  padding: 0;
  border: 2px solid #f008;
}
.floatingPlayerSelect{
  position: absolute;
  bottom: -10%;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  font-size: 1.2em;
}
.floatingSelect{
  position: absolute;
  margin-top: -15px;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  font-size: 1.2em;
}
select{
  background: #4cf;
  text-align: center;
  color: #112;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-family: arial, tahoma;
  font-weight: 700;
  border: 1px solid white;
}
#numContestants{
  font-size: 18px;
}
.picksCompleteButton{
  height: 50px;
  margin-bottom: -15px;
  cursor:pointer;
}
.picksComplete{
  color: #f44;
  font-size: 26px;
}
.statusMessage{
  color: #3ff;
  font-size: 24px;
}
.results{
  color: #fff;
  font-size: 28px;
}
</style>
