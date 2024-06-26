<script lang="ts">
    import ThemeSwitcher from "./ThemeSwitcher.svelte";
</script>

<div class="flex justify-between mb-4 not-prose">

    <div role="tablist" class="">
        <a role="tab" class="btn btn-active no-animation btn-sm" href="/">Board</a>
        <a role="tab" class="btn btn-sm" href="https://blog.darklynx.org">Journal</a>
    </div>

    <ThemeSwitcher themeOptions={["dark", "light"]}/>
</div>