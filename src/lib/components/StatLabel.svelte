<script>
    export let icon
    export let label
    export let outlined = false
</script>

{#if !outlined}
    <div class="badge badge-lg flex flex-row">
        <img src={icon} alt={`${label} icon`} class="w-5 h-5 m-0"/>
        <div class="ml-0.5">{label}</div>
    </div>
{:else}
    <div class="badge badge-lg badge-outline flex flex-row">
        <img src={icon} alt={`${label} icon`} class="w-5 h-5 m-0"/>
        <div class="ml-0.5">{label}</div>
    </div>
{/if}
