<script>
    import { createEventDispatcher } from "svelte";

    // props

    export let tid = "svelte";
    export let name = "123";
    export let done = false;

    let mouseIn = false;
    let btnStyle = "none";
    const handleMouse = (inFlage) => {
        mouseIn = inFlage;
        btnStyle = mouseIn ? "inline" : "none";
    };

    const dispatch = createEventDispatcher();
    const handleDelete = () => {
        dispatch("delete", {
            tid: tid,
        });
    };
    const handleCheck = () => {
        done = !done;
        dispatch("check", {
            tid: tid,
            done: done,
        });
    };
</script>

<li
    on:mouseleave={() => handleMouse(false)}
    on:mouseenter={() => handleMouse(true)}
>
    <label>
        <input type="checkbox" checked={done} on:change={handleCheck} />
        <span>{name}</span>
    </label>
    <button
        class="btn btn-danger"
        style="display: {btnStyle}"
        on:click={handleDelete}
    >
        删除
    </button>
</li>

<style>
    .btn {
        display: inline-block;
        padding: 4px 12px;
        margin-bottom: 0;
        font-size: 14px;
        line-height: 20px;
        text-align: center;
        vertical-align: middle;
        cursor: pointer;
        box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
            0 1px 2px rgba(0, 0, 0, 0.05);
        border-radius: 4px;
    }

    .btn-danger {
        color: #fff;
        background-color: #da4f49;
        border: 1px solid #bd362f;
    }

    .btn-danger:hover {
        color: #fff;
        background-color: #bd362f;
    }

    .btn:focus {
        outline: none;
    }

    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label {
        float: left;
        cursor: pointer;
    }

    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top: -1px;
    }

    li button {
        float: right;
        display: none;
        margin-top: 3px;
    }

    li:before {
        content: initial;
    }

    li:last-child {
        border-bottom: none;
    }
</style>
