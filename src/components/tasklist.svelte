<script lang="ts">
    let tasks: any = [];

    function addTask(task: any){
        tasks = [...tasks, {text: task, completed: false}];
    }

    function removeTask(index: any){
        tasks = tasks.filter((_:any, i:any) => i !== index);
    }

    function toggleTask(index: any){
        tasks = tasks.map((task:any, i:any) => i === index ? {...task, completed: !task.completed}:task);
    }

    let newTask = "";
    let error: any = null;

    function handleSubmit(event: any){
        event.preventDefault();

        if(newTask.trim() === ""){
            error = "Task description cannot be empty";
        } else{
            addTask(newTask);
            newTask = "";
            error = null;
        }
        
    }
</script>

<div class="tasklist">
    <h1>What do you need to do?</h1>
    <form on:submit={handleSubmit}>
        <input bind:value={newTask} placeholder="Enter a task">
        <button class="add-button" type="submit">Add</button>
    </form>
    {#if error}
        <p class="error-message">{error}</p>
    {/if}
    <ul>
    {#each tasks as task,i}
        <li class:completed={task.completed} on:click={() => toggleTask(i)} on:keydown={() => toggleTask(i)}>
            {task.text}
            <button class="remove-button" on:click={() => removeTask(i)}>Remove</button>
        </li>
    {/each}
    </ul>
</div>

<style>
    .tasklist{
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    form{
        display: flex;
        flex-direction: column;
        width: 560px;
    }

    input{
        padding: .4rem;
        border: none;
        border-bottom: 1px solid rgb(85, 85, 85);
        background-color: transparent;
        color: #fffdf2;
    }

    ::placeholder{
        color:#fffdf2;
    }

    input:focus{
        outline: none;
    }
    
    .add-button{
        background: transparent;
        margin-top: 1rem;
        border: 2px dashed rgb(85, 85, 85);
        padding: 1rem;
        font-size: 1.2rem;
        font-weight: 600;
        color:#2b2b2b;
    }
    button:hover{
        cursor: pointer;
    }

    ul{
        list-style-type: none;
        margin: 0;
        padding: 0;
        width: 60%;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 1rem;
    }

    li{
        border-bottom: 1px solid rgb(85, 85, 85);
        padding: .8rem;
        width: 530px;
        margin: .4rem;
        display: flex;
        justify-content: space-between;
        color:#fffdf2;
    }

    .remove-button{
        background-color: transparent;
        border: 1px dashed;
        color: #2b2b2b;
    }
    h1{
        color:#fffdf2;
    }
</style>