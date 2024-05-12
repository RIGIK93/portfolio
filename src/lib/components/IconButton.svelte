<script>
    export let href;
    export let icon;
</script>

<a {href} class="btn btn-sm btn-square btn-primary">
    <img src={icon} alt={`${icon} icon`} class="w-6 h-6 m-0"/>
</a>