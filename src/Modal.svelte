<script>
    export let showModal = true;
</script>

{#if showModal}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="bg" on:click>
        <div class="modal">
            <slot></slot>
        </div>
    </div>
{/if}

<style>
    .bg {
        width: 100%;
        height: 100%;
        position: fixed;
        background: rgba(0, 0, 0, 0.8);
        z-index: 1;
    }

    .modal {
        padding: 20px;
        border-radius: 10px;
        width: 200px;
        text-align: center;
        margin: 10% auto;
        background: #fff;
        font-size: 20px;

        border: 2px solid #108ff0;
        outline: max(2px, 0.15em) solid #108ff0;
  		outline-offset: max(2px, 0.15em);
    }
</style>

