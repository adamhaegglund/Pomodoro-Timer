<script lang="ts">
    
    let timeRemaining = 25*60;
    let timeShortBreak = 5*60;
    let timeLongBreak = 10*60;
    let intervalId: any;
    let pause = false;
    let timerRunning = false;
    let cycles = 0;

    function startTimer(){
        timerRunning = true;
        intervalId = setInterval(() => {
            timeRemaining--;
            if(timeRemaining <= 0){
                clearInterval(intervalId);
                alert('Time is up!')
                cycles++;
                pause = true;
            }
        }, 1000);
    }

    function stopTimer(){
        clearInterval(intervalId);
        timerRunning = false;
    }
    
    function resetTimer(){
        clearInterval(intervalId);
        timerRunning = false;
        timeRemaining = 25*60;
    }

    function startPauseTimer(){
        if(cycles % 3 == 0){
            intervalId = setInterval(() => {
                timeLongBreak--;
                if(timeLongBreak <= 0){
                    clearInterval(intervalId);
                    pause = false;
                }
            }, 1000);
        }else{
            intervalId = setInterval(() => {
                timeShortBreak--;
                if(timeShortBreak <= 0){
                    clearInterval(intervalId);
                    pause = false;
                }
            }, 1000);
        }
    }
</script>


<div class="timer">
    <div class="timer-container">
    {#if !pause}
        <h4>{Math.floor(timeRemaining / 60)}:{('0' + (timeRemaining % 60)).slice(-2)}</h4>
        <div class="buttons">
            
            {#if !timerRunning}
                <button on:click={startTimer} disabled={timerRunning}>Start</button>
                {#if timeRemaining != 25*60}
                <button on:click={resetTimer}>Reset</button>    
                {/if}
                {:else}
                <button on:click={stopTimer}>Stop</button>
            {/if}
            
        </div>
    {:else if cycles % 3 == 0}
        {Math.floor(timeLongBreak / 60)}:{('0' + (timeLongBreak % 60)).slice(-2)}
        <button on:click={startPauseTimer}>Start</button>
    {:else}
        {Math.floor(timeShortBreak / 60)}:{('0' + (timeShortBreak % 60)).slice(-2)}
        <button on:click={startPauseTimer}>Start</button>
    {/if}
    </div>
</div>

<style>
    .timer{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100%;
    }

    .timer-container{
        width: 500px;
        background-color: #f88278;
        margin-top: 2rem;
        padding: 2rem;
        border-radius: .3rem;
    }

    .timer h4{
        text-align: center;
        font-size: 3rem;
        letter-spacing: .2rem;
        color: #fffdf2;
        font-weight: 400;
    }

    .buttons{
        display: flex;
        justify-content: center;
    }
    button{
        background-color: #fffdf2;
        border: none;
        border-radius: .2rem;
        width: 100px;
        color: #f88278;
        margin: 0rem 1rem 0rem 1rem;
        padding: .4rem;
    }
    button:hover{
        cursor: pointer;
    }    
</style>