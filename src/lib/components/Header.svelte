<script lang="ts">
    import ThemeSwitcher from "./ThemeSwitcher.svelte";
</script>

<div class="flex justify-between mb-4 not-prose">

    <div role="tablist" class="">
        <a role="tab" class="btn btn-active no-animation btn-sm" href="/">Board</a>
        <div class="indicator">
            <span class="indicator-item badge badge-secondary badge-sm">Soon!</span> 
            <a role="tab" class="btn btn-disabled btn-sm" href="/">Journal</a>
        </div>
    </div>

    <ThemeSwitcher themeOptions={["dark", "light"]}/>
</div>