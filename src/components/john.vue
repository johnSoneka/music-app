<template>
  <div>
        <h1>{{displayDays}}</h1>
        <h1>{{displayHours}}</h1>
        <h1>{{displayMinutes}}</h1>
        <h1>{{displaySeconds}}</h1>
        {{today}}
       
        
    </div>
</template>
<script>
export default {
    name: "john",
    data() {
        return{
            displayDays: 0,
            displayHours: 0,
            displayMinutes: 0,
            displaySeconds: 0,
            today:{}
        }
    },
    props: ["year","month","date", "hour", "minute","second", "millisecond"],
    computed: {
        _seconds: () => 1000,
        _minutes(){
            return this._seconds * 60
        },
        _hours(){
            return this._minutes* 60
        },
        _days(){
            return this._hours * 24
        },
        end(){
            return new Date(
            this.year,
            this.month,
            this.date,
            this.hour,
            this.second,
            this.millisecond);
        }
    },
    mounted(){
        this.showRemaining()
    },
    methods:{
        showRemaining(){
            const timer = setInterval(() =>{
                const now = new Date();            
                //const end = new Date(2020, 7, 22, 20, 20, 20, 20);
                const distance = this.end.getTime() - now.getTime(); 
                this.today = distance;
                if(distance < 0){
                    clearInterval(timer);
                    return;
                }

                const days = Math.floor(distance / this._days);
                
                const hours = Math.floor((distance % this._days) / this._hours);
                const minutes = Math.floor((distance % this._hours) / this._minutes);
                const seconds = Math.floor((distance % this._minutes) / this._seconds);
                this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
                this.displaySeconds= seconds < 10 ? '0' + seconds : seconds;
                this.displayHours = hours < 10 ? '0' + hours : hours;
                this.displayDays = days < 10 ? '0' + days : days;
            })
        }
    }
}
</script>