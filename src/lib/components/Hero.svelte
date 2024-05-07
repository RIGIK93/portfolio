<script lang="ts">
    import { onMount } from 'svelte';

    let canvas: HTMLCanvasElement;
    let wrapper: HTMLElement;

    // Fixing Blurry Canvas
        // https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas
        function unblur_canvas(canvas: HTMLCanvasElement, ctx: CanvasRenderingContext2D) {
            const dpr = window.devicePixelRatio;
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * dpr;
            canvas.height = rect.height * dpr;
            ctx.scale(dpr, dpr);
            canvas.style.width = `${rect.width}px`;
            canvas.style.height = `${rect.height}px`;
        }

        function setup_canvas(canvas: HTMLCanvasElement, wrapper: HTMLElement) {
            let wrapper_shape = wrapper.getBoundingClientRect();
            console.log(wrapper_shape.width)
            console.log(canvas)

            canvas.width = wrapper_shape.width
            canvas.height = wrapper_shape.height


            // resize is not required anymore, since changing position to "relative" 
            // on the header somehow fixed the issue.
            // canvas.style.left = wrapper_shape.left.toString() + "px"
            // canvas.style.top = wrapper_shape.top.toString() + "px"

            // See issue #2: https://github.com/RIGIK93/portfolio/issues/2
            // for some reason unblur_canvas function did not respond to the changes in
            // canvas.width and canvas.height unless the css is reset.
            canvas.style.width = ""
            canvas.style.height = ""

            unblur_canvas(canvas, canvas.getContext("2d") as CanvasRenderingContext2D)
            // console.log("called it")
        }

    // $: setup_canvas(canvas, wrapper)

    onMount(() => {
        // const PADDING = 10

        // const canvas = document.getElementById("stars") as HTMLCanvasElement
        const ctx = canvas.getContext("2d") as CanvasRenderingContext2D

        

        // window.addEventListener("resize", () => setup_canvas(document.getElementById("stars")! as HTMLCanvasElement, document.getElementById("header")!)) 
        setup_canvas(canvas, wrapper)

        const STAR_DENSITY = 1/500
        const STAR_SIZE = 5;
        const STAR_COUNT = STAR_DENSITY / STAR_SIZE * (canvas.width * canvas.height)

        interface Vector2 {
            x: number,
            y: number
        }

        interface Star {
            pos: Vector2
            opacity: number
        }

        function create_star(): Star {
            return {
                pos: {
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height
                },
                opacity: Math.random() 
            }
        }

        function draw_star(s: Star): void {
            ctx.fillStyle = `rgba(255,255,255, ${s.opacity})`
            ctx.shadowBlur = 5
            ctx.shadowColor = `rgba(255,255,255, ${s.opacity})`
            ctx.fillRect(s.pos.x, s.pos.y, STAR_SIZE, STAR_SIZE);
        }

        let stars: Star[] = []
        for (let i = 0; i < STAR_COUNT; i++) {
            stars.push(create_star())
        }

        function redraw_stars(stars: Star[]): void {
            ctx.clearRect(0, 0, canvas.width, canvas.height); // clear canvas
            stars.forEach(s => draw_star(s))
        }

        const TICK = 1
        const DISSIPATION_SPEED = 0.000314 // Oppacity / tick
        const interval_id = setInterval(() => {
            if (!canvas) {
                console.error("CANVAS IS NULL. DROPPING STAR LOOP")
                clearInterval(interval_id)
            }

            for (let i = 0; i < stars.length; i++) {
                if (stars[i].opacity <= TICK * DISSIPATION_SPEED)
                    stars[i] = create_star()
                stars[i].opacity -= TICK*DISSIPATION_SPEED
            }

            redraw_stars(stars)
        }, TICK)
    })
</script>

<svelte:window on:resize={() => setup_canvas(canvas, wrapper)} />

<header id="header" bind:this={wrapper} class="relative h-80 md:h-40 bg-black rounded-md flex">
    <h1 class="text-white self-center justify-self-center text-center my-0 mx-auto z-10 bg-black">Greetings, Adventurer!</h1>
    <canvas id="stars" bind:this={canvas} class="absolute top-0 left-0"></canvas>
</header>