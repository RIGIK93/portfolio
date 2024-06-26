
<script lang="ts">
    import Hint from "$lib/components/Hint.svelte";
    import StatLabel from "$lib/components/StatLabel.svelte";
    import IconButton from "$lib/components/IconButton.svelte";
    import Hero from "$lib/components/Hero.svelte"
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";

    import CPP_SVG from "$lib/assets/svg/cpp.svg"
    import GITHUB_SVG from "$lib/assets/svg/github.svg"
    import LINKEDIN_SVG from "$lib/assets/svg/linkedin.svg"
    import BACK_TO_SYNC from "$lib/assets/back_to_sync.avif"
    import AMPHIBIAN_WORLD from "$lib/assets/amphibian_world.png"

    // Using https://img.icons8.com/
    // Use color/icon_name to get colored icon
    // prefix spaces with _ or -
    // use -filled to get filled icon
    // Use AAAAAA/icon_name to get white icon
    function fetch_svg(name: string): string {
        return `https://img.icons8.com/${name}`
    }

    interface Stat {
        label: string,
        icon: string,
        points: number
    }

    let stats: Stat[] = [
        {
            icon: CPP_SVG,
            label: "C++",
            points: 1
        },
        {
            icon: fetch_svg("AAAAAA/unity"),
            label: "Unity",
            points: 2
        },
        {
            icon: fetch_svg("color/typescript"),
            label: "TypeScript",
            points: 4,
        },
        {
            icon: fetch_svg("color/python"),
            label: "Python",
            points: 1
        },
        {
            icon: fetch_svg("color/48/java-coffee-cup-logo--v1.png"),
            label: "Java",
            points: 1
        },
        {
            icon: fetch_svg("nolan/64/godot.png"),
            label: "Godot",
            points: 0.5
        },
        {
            icon: "https://upload.wikimedia.org/wikipedia/commons/d/d5/Rust_programming_language_black_logo.svg",
            label: "Rust",
            points: 1
        }
    ]

    stats.sort((a,b) => b.points - a.points)

    function get_stat(label: string): Stat {
        let stat = stats.find(s => s.label == label)
        if (stat == undefined)
            throw `Stat with the name "${label}" does not exist!`
        return stat
    }

    interface ReIconButton {
        icon: string,
        href: string
    }

    interface Card {
        image: string
        title: string
        description: string
        links: ReIconButton[]
        stats: Stat[]
    }

    let cards: Card[] = [
        {
            title: "Back To Sync",
            description: `A game I developed with my friends over the week of "2022 UNC Collegiate Game Jam."`, // This week-long voyage taught me how to collaborate and match deadlines, use 2D tiles, animate sprites, use state machines and operate player controllers.
            image: BACK_TO_SYNC,
            links: [
                {
                    icon: fetch_svg("pulsar-gradient/48/itch-io.png"),
                    href: "https://rigik93.itch.io/back-to-sync"
                }
            ],
            stats: [
                {
                    icon: get_stat("Unity").icon,
                    label: "Unity",
                    points: 1,
                }
            ]
        },
        {
            title: "Amphibian World",
            description: "Interactive website about amphibians, developed for my biology class.",
            image: AMPHIBIAN_WORLD,
            links: [{
                icon: fetch_svg('internet'),
                href: "https://amphibia.darklynx.org/"
            }],
            stats: [{
                icon: get_stat('TypeScript').icon,
                label: "TypeScript",
                points: 1,
            }]
        }
    ]

    // TODO
    // https://stackoverflow.com/questions/30143082/how-to-get-color-value-from-gradient-by-percentage-with-javascript
</script>

<svelte:head>
    <title>Maxim's Fantasy Portfolio</title>
    <meta name="description" content="Welcome to my fantasy portfolio, the place where I reveal the thorny and buggy path of my tech adventure...">

    <meta property="og:title" content="Maxim's Fantasy Portfolio">
    <meta property="og:description" content="Hey! Check out my portfolio!"/>
    <meta property="og:type" content="website" />
    <meta property="og:image" content="https://darklynx.org/og_cover.png"/>
</svelte:head>


<main class="mx-auto px-5 pt-10 md:px-0 md:w-1/2 prose font-mono">

    <Header></Header>
   
    <Hero></Hero>

    <!-- <nav></nav> -->

    <p>I am Maxim and [You] have stumbled upon my tech portfolio!</p>
    <!-- Maxim welcomes yee who have stumbled upon thee portfolio! -->

    <!-- Character Description -->
    <article class="container">
        <div class="divider divider-start">Character Description ℹ️</div>
        <p>
            The path may be full of bugs and winding trails ending in countless dead ends, 
            but who is going on an adventure expecting it to be easy? 
            Challenge is the intrinsic part that makes the adventure interesting.
        </p>
        <p>
            This adventure is also a magical one. 
            “Any sufficiently advanced technology is indistinguishable from magic” — Athur C. Clarke.
            I believe that programming is as close as we can get to magic in this world. 
            It is simply magical to program something: an exciting, magical adventure.
        </p>
    </article>

    <!-- Character Stats -->

    <article class="container">
        <div class="divider divider-start">Character Stats ⚔️ <Hint txt="Character Stats are the skills of character [Maxim], essential for his coding adventures. 1 PP (Project Point) is awarded for every 1,000 lines of code written using some skill."/></div>
        <!-- svelte. FORMAT: Icon Stat_Name (BIG SPACe) PROFICIENCY_LEVEL -->
        <div class="flex flex-col gap-2">
            {#each stats as stat}
                <div class="flex h-5 flex-grow justify-between">
                    <StatLabel
                        outlined={true}
                        icon={stat.icon}
                        label={stat.label}
                    />
                    <div>{stat.points} PP</div> <!-- class="text-[rgb(1,1,1)]" -->
                </div>
            {/each}
        </div>
        
    </article>


    <article>
        <!-- Quests -->
        <!-- 
            Note: Each Quest should list a proficiency and by how much it has boosted the specific proficiency
        -->
        <div class="divider divider-start pt-5">Quests 📜 <Hint txt="Quests are projects [Maxim] contributed to. Quests boost PP (Project Points) of certain [Character Stats]. The stat and the number of PP contributed by a certain [Quest] is written bellow each [Quest]."/></div>

    </article>

    <!-- Campaings (Companies/Experience) -->
    <!-- Use Daisy UI "Timeline with icon snapped to the start" -->
    <!-- https://daisyui.com/components/timeline/ -->
    <!-- title: [Company Name] | [Position] -->

    <!-- Scrolls 📖 (Blog Posts) -->
</main>

<div class="flex justify-center py-3">
    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-5">

        {#each cards as card}
            <div class="card col-span-1 mx-5 sm:mx-0 sm:w-60 card-compact bg-base-100 shadow-xl font-mono">
                <figure><a href={card.links[0].href}><img class="img-btn" src={card.image} alt={`${card.title} Cover Image`} /></a></figure>
                <div class="card-body">
                <h2 class="card-title">
                    {card.title}
                </h2>
                <p>{card.description}</p>
                <div class="card-actions justify-start">
                    {#each card.links as link}
                        <IconButton icon={link.icon} href={link.href} />
                    {/each}
                </div>
                <div class="card-actions justify-end">
                    {#each card.stats as stat}
                        <StatLabel 
                            outlined={true} 
                            icon={stat.icon} 
                            label={stat.points == 0 ? stat.label 
                                                    : `${stat.points >= 0 ? "+" : "-"}${stat.points}`}
                        />
                    {/each}
                    <!-- <StatLabel outlined={true} icon={fetch_svg("pulsar-gradient/48/itch-io.png")} label="+5" />
                    <StatLabel outlined={true} icon={CPP_SVG} label="+5" /> -->
                </div>
                </div>
            </div>
        {/each}
    
    </div>
</div>

<footer class="mx-auto px-5 pt-5 pb-10 md:px-0 md:w-1/2 prose font-mono">
    <div class="divider divider-start">Contacts 🦉</div>
    <!-- pulsar-line/48/FFFFFF/mail.png -->
    <aside class="">
        Need a hire or someone to clean a [Goblin] infestation? Send me an e-mail <IconButton icon={fetch_svg("pulsar-line/48/mail.png")} href="mailto:maxim.peniaz@gmail.com" /> and I'll make sure to read it immediately after the owl delivers it. You can also find me on 
        <IconButton icon={GITHUB_SVG} href="https://github.com/RIGIK93" />
        <IconButton icon={LINKEDIN_SVG} href="https://www.linkedin.com/in/maxim-peniaz-1008a7237/"/>
        <IconButton icon={fetch_svg("pulsar-gradient/48/itch-io.png")} href="https://rigik93.itch.io/"/>
        .
    </aside>
    <!-- Need help clearing orc infestations or you're just interested in hiring me? Just send me an email, will ya'? -->
</footer>

<Footer />

<style>
    /* @media(hover:hover) { */
        .img-btn:hover {
            /* background-color: var(--fallback-b3,oklch(var(--b3)/var(--tw-bg-opacity))); */
            opacity: 0.7;
        }
    /* } */
</style>
