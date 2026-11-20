<script>
    import { fade } from "svelte/transition";
    import { onMount } from "svelte";

    let screenWidth = $state(1000);
    let scrollY = $state(0);
    const letters = "Plush".split("");

    let settled = $state(false);
    onMount(() => {
        setTimeout(() => {settled = true}, 1500)
    })
</script>

<svelte:head>
    <title>Plush</title>
</svelte:head>

<svelte:window bind:innerWidth={screenWidth} bind:scrollY={scrollY}></svelte:window>

<style>
    /* Parent anchor container */
    #titleBox {
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 180px;
        z-index: 99;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #title {
        position: relative; /* Positioned relative to #titleBox */
        font-size: 190px;
        font-weight: 200;
        display: flex;
        margin: 0;
    }

    #tagLogo {
        position: absolute; /* Positioned relative to #titleBox */
        display: flex;
        z-index: 101;
        width: 80px;
        left: 96%;
        top: 40%;
        transform: translate(-50%, -50%) scale(1.45);
    }

    #desc {
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 50px;
        text-align: center;
        z-index: 99;
        span {
            color: rgb(237, 233, 178);
            font-weight: 600;
        }
        font-size: 20px;
        font-weight: 400;
    }

    .char {
        color: rgb(178, 220, 237);
        user-select: none;
        display: inline-block;
        opacity: 0;
        transform: translateY(-120px) scale(1);
        animation: flyAndSettle 0.9s cubic-bezier(0.22, 1, 0.36, 1) forwards;
        animation-delay: calc(var(--index) * 80ms + 1000ms);
    }

    @keyframes flyAndSettle {
        0% {
            opacity: 0;
            transform: translateY(-120px) scale(1);
            color: rgb(178, 220, 237);
        }
        80% {
            opacity: 1;
            transform: translateY(0) scale(1);
            color: rgb(178, 220, 237);
            font-weight: 200;
        }
        100% {
            opacity: 1;
            transform: translateY(0) scale(1.1);
            color: rgb(216, 239, 250);
            font-weight: 500;
        }
    }

    #shark {
        z-index: 100;
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 55%;
        max-width: 500px;
        transition: all 0.5s ease-in-out;
        animation: bobShark infinite ease-in-out 5s;
    }

    @media screen and (max-width: 750px) {
        #titleBox {
            top: 180px;
        }
        #title {
            font-size: 120px;
        }
        #tagLogo {
            left: 97.15%;
            top: 40%;
            transform: translate(-50%, -50%) scale(1);
        }
        #shark {
            max-width: 300px;
            top: 46.5%;
        }
    }

    #initDirection {
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 600px;
        font-size: 70px;
        z-index: 99;
        opacity: 0;
        animation: fadeInArrow 2.5s ease-in-out 0.8s forwards, bobArrow 2s infinite ease-in-out 0.8s;
        user-select: none;
    }

    @keyframes fadeInArrow {
        0%, 40% { opacity: 0; }
        100% { opacity: 1; }
    }

    @keyframes bobArrow {
        0%, 100% {
            top: 600px;
            color: white;
        }
        50% {
            top: 610px;
            color: rgb(216, 239, 250);
        }
    }

    @keyframes bobShark {
        0%, 100% {
            transform: translate(-50%, -50%) rotate(-1deg) translateY(0px);
        }
        50% {
            transform: translate(-50%, -50%) rotate(1deg) translateY(10px);
        }
    }

    #bodyContent {
        position: relative;
        top: 900px;
        background-color: black;
        width: 100%;
        text-align: center;
    }
</style>

<div id="titleBox" style:opacity={1-(scrollY)/300}>
    <h1 id="title" translate="no">
        {#each letters as char, i}
            <span class="char" style="--index: {i}">{char}</span>
        {/each}
    </h1>
    {#if settled}<img transition:fade id="tagLogo" src="/images/tag.webp" alt="" />{/if}
</div>

<h2 id="desc" style:opacity={1-(scrollY)/100}>Build <span>cute projects</span> get <span>cute prizes</span></h2>

<img id="shark" style:opacity={1-(scrollY)/400} src="/images/blahaj.webp" alt="Shark plushie" />

<span aria-hidden="true" id="initDirection" class="material-symbols-outlined" translate="no">
    {screenWidth <= 750 ? "swipe_down" : "arrow_circle_down"}
</span>

<div id="bodyContent">
    <h3>Die</h3>
</div>