<script>
    import { createEventDispatcher } from "svelte";
    import { nanoid } from "nanoid";

    let val = "";
    const dispatch = createEventDispatcher();
    const handleAdd = (e) => {
        if (e.key == "Enter") {
            dispatch("add", {
                tid: nanoid(),
                name: val,
                done: false,
            });
            val = "";
        }
    };
</script>

<div class="todo-header">
    <input
        type="text"
        placeholder="请输入你的任务名称，按回车键确认"
        bind:value={val}
        on:keyup={handleAdd}
    />
</div>

<style>
    .todo-header input {
        width: 560px;
        height: 28px;
        font-size: 14px;
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 4px 7px;
    }

    .todo-header input:focus {
        outline: none;
        border-color: rgba(82, 168, 236, 0.8);
        box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
            0 0 8px rgba(82, 168, 236, 0.6);
    }
</style>
