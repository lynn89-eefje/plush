<script>
    import { cubicOut } from "svelte/easing";
    import { fly } from "svelte/transition";
    import { onMount } from "svelte";
    import Login from "#lib/components/login.svelte";

    let screenWidth = $state(1000);
    let scrollY = $state(0);
    const letters = "Plush".split("");

    const displayList = ["blahaj_hoodie", "capybara_lamp", "koala_lamp", "whale_lamp", "bunny_lamp", "aftonsparv_sweatshirt", "ceiling_plush", "redpanda_ikea", "djungleskog_shirt", "orangutan_ikea", "capybara_plush"]
    let currDisplay = $state(displayList[0])

    let settled = $state(true); // usually set to false
    onMount(() => {
        const loop = setInterval(() => {
            let index = displayList.indexOf(currDisplay);
            if (index == displayList.length-1) {
                currDisplay = displayList[0];
            }
            else {
                currDisplay = displayList[index + 1];
            }
        }, 2000)
    });
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
        position: absolute;
        user-select: none;
        display: flex;
        z-index: 101;
        width: 80px;
        left: 96%;
        top: 40%;
        transform: translate(-50%, -50%) scale(1.45);
        transition: opacity 0.4s ease-in-out;
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
        color: var(--blue);
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
        top: 53%;
        max-width: 500px;
        transition: all 0.5s ease-in-out;
        animation: bobShark infinite ease-in-out 5s;
        user-select: none;
    }

    #animalBanner {
        position: absolute;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 0;
    }

    @keyframes pulseShape {
        0%, 100% {
            opacity: 1;
            transform: scale(1);
        }
        50% {
            opacity: 0.6;
            transform: scale(0.975);
        }
    }

    #collectionLeft {
        position: fixed;
        left: 0;
        bottom: 0;
        z-index: 98;
        display: flex;
        pointer-events: none;
    }

    #collectionLeft img, #collectionRight img {
        position: relative;
        user-select: none;
        max-height: 200px;
        animation: pulseShape 3s infinite ease-in-out;
        animation-delay: calc(var(--index) * 800ms + 1000ms);
    }

    #collectionRight {
        position: fixed;
        right: 0;
        bottom: 0;
        z-index: 98;
        display: flex;
        pointer-events: none;
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
            top: 45%;
        }
        #collectionLeft, #collectionRight {
            display: none;
        }
    }

    #initDirection {
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 630px;
        font-size: 70px;
        z-index: 99;
        user-select: none;
        transition: opacity 0.5s ease-in-out;
        animation: bobArrow 2s infinite ease-in-out;
    }

    @keyframes bobArrow {
        0%, 100% {
            top: 630px;
            color: white;
        }
        50% {
            top: 640px;
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
        background-color: red;
        width: 100%;
        text-align: center;
        z-index: 105;
    }

    #login {
        position: fixed;
        right: 20px;
        top: 20px;
    }

    #prizeCarousel {
        position: relative;
        width: 90%;
        max-width: 400px;
        height: 100%;
        margin: 0 auto;
        overflow-x: clip;
        
        img {
            position: absolute;
            transform: translate(-50%, -50%);
            left: 50%;
            top: 50%;
            max-width: 100%;
            animation: rotateAround 8s infinite;
            animation-timing-function: linear;
        }
        .item {
            max-width: 100%;
            animation: none;
            transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
        }
    }

    @media screen and (max-width: 750px) {
        #login {
            transform: translate(-50%, -50%);
            left: 50%;
            top: 72%;
        }
    }

    @keyframes rotateAround {
        0% {
            transform: translate(-50%, -50%) rotate(0deg);
            opacity: 0.8
        }
        50% {
            transform: translate(-50%, -50%) rotate(180deg);
            opacity: 0.3
        }
        100% {
            transform: translate(-50%, -50%) rotate(360deg);
            opacity: 0.8;
        }
    }
</style>

<div id="titleBox" style:top={180-(scrollY/20)}px>
   <h1 id="title" translate="no" aria-label="Plush">
        {#each letters as char, i}
            <span aria-hidden="true" class="char" style="--index: {i}">{char}</span>
        {/each}
    </h1>
    <img id="tagLogo" style:opacity={settled ? 1 : 0} src="/images/tag.webp" alt="Hack Club logo" />
</div>

<h2 id="desc" style:opacity={1-(scrollY)/600}>Build <span>cute projects</span> get <span>cute prizes</span></h2>

<img id="shark" src="/images/blahaj.webp" alt="Mascots riding shark plushie" />

<div id="login" style:display={scrollY > 800 ? "none" : "block"}>
    <Login />
</div>

{#if scrollY < 370}
<div id="collectionLeft">
    <img transition:fly={{x: -200, easing: cubicOut, duration: 2400}} src="/images/shapes/shape2.webp" alt="" style="--index: 0; bottom: 150px; left: 100px;"/>
    <img transition:fly={{x: -200, easing: cubicOut, duration: 1200}} src="/images/shapes/shape3.webp" alt="" style="--index: 1; scale: 0.4; left: -240px;"/>
    <img transition:fly={{x: 200, easing: cubicOut, duration: 1800}} src="/images/shapes/shape5.webp" alt="" style="--index: 2; scale: 0.15; bottom: 450px; left: -400px; rotate: 190deg"/>
    <img transition:fly={{x: -200, easing: cubicOut, duration: 1900}} src="/images/shapes/shape4.webp" alt="" style="--index: 3; scale: 0.25; bottom: 300px; left: -650px;"/>
</div>
{/if}
{#if scrollY < 370}
<div id="collectionRight">
    <img transition:fly={{x: 200, easing: cubicOut, duration: 1800}} src="/images/shapes/shape1.webp" alt="" style="--index: 1; scale: 0.7; bottom: 200px; right: -350px;"/>
    <img transition:fly={{x: 200, easing: cubicOut, duration: 2200}} src="/images/shapes/shape5.webp" alt="" style="--index: 0; scale: 0.3; bottom: 0px; right: -200px;"/>
    <img transition:fly={{x: 200, easing: cubicOut, duration: 2200}} src="/images/shapes/shape4.webp" alt="" style="--index: 2; scale: 0.15; bottom: -40px; right: 50px;"/>
</div>
{/if}

<span 
    aria-hidden="true" 
    id="initDirection" 
    class="material-symbols-outlined" 
    style:opacity={settled ? Math.max(0, 1 - (scrollY) / 300) : 0}
    translate="no"
>
    {screenWidth <= 750 ? "swipe_down" : "arrow_circle_down"}
</span>

<div id="bodyContent" style:background-color="black">
    <img src="/images/animalBanner.webp" id="animalBanner" alt=""/>
    {#if screenWidth > 750}
    <div aria-hidden="true" style:height=200px></div>
    {:else}
    <div aria-hidden="true" style:height=80px></div>
    {/if}
    <div style:font-size=50px style:font-family="Playwrite DK Loopet, Cal Sans, Montserrat" style:font-weight=900 style:color="rgb(237, 233, 178)"><span style:color="rgb(237, 233, 178)">about</span><span aria-hidden="true" style:color="white">.</span></div>
    <p style:margin-left=30px style:margin-right=30px>Build websites, games, and art about something toy-themed or cute. <strong>Get plushies, lamps, merch, and more!</strong></p>
    
    <div style="display: block; width: 90%; height: 300px; margin: {screenWidth > 750 ? '100px' : '50px'} auto 0 auto;">
        <div id="prizeCarousel" aria-label="Collection of merch items and prizes">
            <img alt="" src="/images/shapes/shape1.webp" />
            {#each displayList as itemName}
                {@const isMerch = itemName.includes("shirt") || itemName.includes("hoodie") || itemName.includes("sweatshirt")}
                <img 
                    class="item" 
                    src="/images/items/{itemName}.webp" 
                    alt="" 
                    style:opacity={currDisplay === itemName ? "1" : "0"} 
                    style:pointer-events={currDisplay === itemName ? "auto" : "none"} 
                    style:transform="translate(-50%, -50%) rotate({isMerch ? 5 : 0}deg)"
                />
            {/each}
        </div>
    </div>
</div>