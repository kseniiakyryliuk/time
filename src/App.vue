<template>
  <div id="app">
    <div class="main-info">
 <p>Current time is  <span class="date">{{ thisT }}</span> </p>
   <p >New year <span class="date"> {{ nYear }} </span></p>
  </div>
  <div class="time">
  <div class="item">
<p v-if="lasttime.days/10<1">0{{lasttime.days}}</p>
<p v-else>{{ lasttime.days}}</p>
<span>day(s)</span>
</div>


<div class="item">
<p v-if="lasttime.hours/10<1">0{{lasttime.hours}}</p>
<p v-else>{{ lasttime.hours}}</p>
<span>hour(s)</span>
</div>

<div class="item">
<p v-if="lasttime.minutes/10<1">0{{lasttime.minutes}}</p>
<p v-else>{{ lasttime.minutes}}</p>
<span>minute(s)</span>
</div>

<div class="item">
<p v-if="lasttime.seconds/10<1">0{{lasttime.seconds}}</p>
<p v-else>{{ lasttime.seconds}}</p>
<span>second(s)</span>
</div>
     
</div>

<div class="list">
<ul>
  <li>Days <b > {{days}} </b></li>
  <li>Hours <b>{{hours}}</b></li>
  <li>Minutes <b>{{minutes}}</b></li>
  <li>Seconds <b>{{seconds}}</b></li>
</ul>

</div>

</div> 
</template>

<script>


export default {
  name: 'App',
data(){
  return{
    nYear:'',
    thisT:'',
 timeDate: '',
 days:'',
 hours:'',
 minutes:'',
 seconds:'',
lasttime:{
  days:"",
  hours:"0",
  minutes:"0",
  seconds: "0"
},

 }},
created() {
                setInterval(this.getNow, 1000);
            },
            methods: {
                getNow: function() {

                const minute = 1000 * 60;
                const hour = minute * 60;
                const day = hour * 24;

              const today = new Date(); 
                          let yearDif=today.getFullYear()+1;   
               const newYear=new Date([`${yearDif}-01-01`,`00:00`]);
               this.nYear=`00:00:00   01.01.${yearDif}`;
                  

this.days=Math.floor(newYear.getTime()/day)-Math.floor(today.getTime()/day);
this.hours=Math.floor(newYear.getTime()/hour)-Math.floor(today.getTime()/hour)-1;
this.minutes=Math.floor(newYear.getTime()/minute)-Math.floor(today.getTime()/minute)
this.seconds=Math.floor(newYear.getTime()/1000)-Math.floor(today.getTime()/1000)

this.lasttime.days=this.days;
this.lasttime.hours=23-today.getHours();

this.lasttime.minutes=59-today.getMinutes();
this.lasttime.seconds=59-today.getSeconds();


let date;
if(today.getDate()/10<1)
date='0'+today.getDate();
else date=today.getDate();

if((today.getMonth()+1)/10<1)
date+='.0'+(today.getMonth()+1)+'.'+today.getFullYear();
else  date+='.'+(today.getMonth()+1)+'.'+today.getFullYear();

  //  date =today.getDate() +'.'+(today.getMonth()+1)+'.'+today.getFullYear();

let time;

if(today.getHours()/10<1)
time='0'+today.getHours();
else time=today.getHours();


if(today.getMinutes()/10<1)
time+=':0'+today.getMinutes();
else   time+=':'+today.getMinutes();



if(today.getSeconds()/10<1)
time+=':0'+today.getSeconds();
else   time+=':'+today.getSeconds();



                   const dateTime =time  +'   '+ date;
                    this.thisT=dateTime;
                  
              
                }



}}
</script>

<style>
body{
  background-color: rgb(211, 175, 228);
}
ul{
  list-style: none;
  }
.item{
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin: 10px;
}
span{
   font-size: 10px;
color: rgb(130, 5, 146);
font-weight: 700;
text-align: center;
text-transform: uppercase;
}
.date{
  color: royalblue;
  font-size: 18px; 
}
.main-info{
  text-align: center;
}
.item p{
  background-color: black;
  color: white;
  border-radius:10px ;
  font-size: 45px;
  padding: 7px;
  margin: 0;
  text-align: center;   
}
.time{
  display: flex;
  justify-content: center;
}
.list{
  text-align: center;
  font-size: 18px;
}

</style>
