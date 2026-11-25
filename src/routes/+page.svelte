
<script>
    import { cubicOut } from "svelte/easing";
    import { fly } from "svelte/transition";
    import { onMount } from "svelte";
    import Login from "#lib/components/login.svelte";

    let screenWidth = $state(1000);
    let scrollY = $state(0);
    const letters = "Plush".split("");

    const displayList = [
        "blahaj_hoodie",
        "bunny_lamp",
        "capybara_lamp",
        "capybara_plush",
        "blahaj_ikea",
        "djungleskog_shirt",
        "ceiling_plush",
        "koala_lamp",
        "blavingad_sweatshirt",
        "orangutan_ikea",
        "aftonsparv_sweatshirt",
        "whale_lamp"
    ];

    let currDisplay = $state(displayList[0]);

    let settled = $state(true); // usually set to false

    onMount(() => {
        const loop = setInterval(() => {
            let index = displayList.indexOf(currDisplay);

            if (index == displayList.length - 1) {
                currDisplay = displayList[0];
            } else {
                currDisplay = displayList[index + 1];
            }
        }, 2000);

        return () => clearInterval(loop);
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
        position: relative;
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

    /* Shark container */
    #sharkContainer {
        z-index: 100;
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 53%;
        width: 100%;
        max-width: 500px;
        animation: bobShark infinite ease-in-out 5s;
        user-select: none;
    }

    /* Main shark image */
    #shark {
        display: block;
        width: 100%;
        height: auto;
    }

    /* Eyes overlay */
    #heidiEyes {
        position: absolute;
        width: 100%;
        height: auto;
        top: 0;
        left: 0;
        pointer-events: none;
        user-select: none;
        animation: heidiEyes 3.5s infinite ease-in-out;
        animation-delay: 2500;
        -webkit-user-drag: none;
        user-select: none;
        -moz-user-select: none;
    }

    #orpheusEyes {
        position: absolute;
        width: 100%;
        height: auto;
        top: 0;
        left: 0;
        pointer-events: none;
        user-select: none;
        animation: heidiEyes 6s infinite ease-in-out;
        -webkit-user-drag: none;
        user-select: none;
        -moz-user-select: none;
    }

    @keyframes heidiEyes {
        0%, 43%, 50%, 100% {
            opacity: 0;
        }
        44%, 49% {
            opacity: 1;
        }
    }

    #animalBanner {
        position: absolute;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 0;
        user-select: none;
    }

    @keyframes pulseShape {
        0%, 100% {
            opacity: 1;
            transform: scale(1);
        }

        50% {
            opacity: 0.6;
            transform: scale(0.93);
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

    #collectionLeft img,
    #collectionRight img {
        position: relative;
        user-select: none;
        max-height: 200px;
        animation: pulseShape 3s infinite ease-in-out;
        animation-delay: calc(var(--index) * 800ms + 2500ms);
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

        #sharkContainer {
            max-width: 400px;
            top: 48%;
        }

        #collectionLeft,
        #collectionRight {
            display: none;
        }
    }

    #initDirection {
        position: fixed;
        transform: translate(-50%, -50%);
        left: 50%;
        top: 610px;
        font-size: 70px;
        z-index: 99;
        user-select: none;
        transition: opacity 0.5s ease-in-out;
        animation: bobArrow 2s infinite ease-in-out;
    }

    @keyframes bobArrow {
        0%, 100% {
            top: 610px;
            color: white;
        }

        50% {
            top: 620px;
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
        top: 950px;
        background-color: red;
        width: 100%;
        text-align: center;
        z-index: 105;

        p {
            margin-left: 30px;
            margin-right: 30px;
        }
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
            animation: rotateAround 16s infinite;
            animation-timing-function: linear;
            user-select: none;
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
            top: 77%;
        }
    }

    @keyframes rotateAround {
        0% {
            transform: translate(-50%, -50%) rotate(0deg);
            opacity: 0.9;
        }

        50% {
            transform: translate(-50%, -50%) rotate(180deg);
            opacity: 0.3;
        }

        100% {
            transform: translate(-50%, -50%) rotate(360deg);
            opacity: 0.9;
        }
    }

    #landingCrates {
        margin: 0 auto;
        z-index: 20;
        display: flex;
        gap: 0px;
        user-select: none;
        -webkit-user-drag: none;
        -moz-user-select: none;

        div {
            width: 50%;
            align-self: center;
        }
    }

    /* Crate floating animation */
    .crateContainer {
        width: 50%;
        height: fit-content;
        align-self: center;
        position: relative;
    }

    .crate {
        width: 400px;
        animation: crateFloat 3s ease-in-out infinite;
        will-change: transform;
    }

    .crate img {
        display: block;
        width: 100%;
        height: auto;
    }

    .crateIkea {
        transform: translateY(40px) translateX(-30%);
    }

    .crateHoodies {
        transform: translateY(-180px) translateX(59%) scale(0.88) rotate(-3deg);
        animation-delay: -1.5s;
    }

    @keyframes crateFloat {
        0%, 100% {
            translate: 0 0;
        }

        50% {
            translate: 0 -10px;
        }
    }
    @media screen and (max-width: 750px) {
        .crateContainer {
            width: 100% !important;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .crate {
            width: 400px;
            max-width: 100%;
        }

        .crateIkea {
            transform: translateY(40px) translateX(-75px);
        }

        .crateHoodies {
            transform: translateY(-180px) translateX(90px) scale(0.88) rotate(-3deg);
        }
    }

    #ideas {
        display: flex;
        flex-direction: row;
    }
    #ideaSide {
        margin-left: 100px;
        margin-top: 100px;
        div {
            margin: 10px;
            border: 4px solid white;
            background-color: rgba(128, 128, 128, 0.227);
            border-radius: 20px;
            padding: 20px;
            width: fit-content;
            font-family: Cal Sans, Host Grotesk;
        }
    }
    @media screen and (max-width: 750px) {
        #ideaSide {
            margin-left: 0;
            margin-top: 30px;
            display: flex;
            flex-direction: column;
            div {
                width: 85%;
                display: block;
                margin: 0 auto;
                margin-bottom: 20px;
            }
        }
    }
</style>

<div id="titleBox" style:top={180-(scrollY/20)}px>
    <h1 id="title" translate="no" aria-label="Plush">
        {#each letters as char, i}
            <span aria-hidden="true" class="char" style="--index: {i}">{char}</span>
        {/each}
    </h1>

    <img
        id="tagLogo"
        style:opacity={settled ? 1 : 0}
        src="/images/tag.webp"
        alt="Hack Club logo"
    />
</div>

<p id="desc" style:opacity={1-(scrollY)/600}>
    Build <span>cute projects</span> get <span>cute prizes</span>
</p>

<!-- Shark and eyes share one animated container -->
<div id="sharkContainer">
    <img
        id="shark"
        src="/images/blahaj.webp"
        alt="A large shark plushie with mascots riding on top"
    />

    <img
        id="heidiEyes"
        src="/images/heidi_eyes.webp"
        alt=""
    />
    <img
        id="orpheusEyes"
        src="/images/orpheus_eyes.webp"
        alt=""
    />
</div>

<div id="login" style:display={(scrollY > 900 || screenWidth < 750) ? "none" : "block"}>
    <Login />
</div>

{#if scrollY < 270}
    <div id="collectionLeft">
        <img
            transition:fly={{x: -200, easing: cubicOut, duration: 2400}}
            src="/images/shapes/shape2.webp"
            alt=""
            style="--index: 0; bottom: 150px; left: 100px;"
        />

        <img
            transition:fly={{x: -200, easing: cubicOut, duration: 1200}}
            src="/images/shapes/shape3.webp"
            alt=""
            style="--index: 1; scale: 0.4; left: -240px;"
        />

        <img
            transition:fly={{x: 200, easing: cubicOut, duration: 1800}}
            src="/images/shapes/shape5.webp"
            alt=""
            style="--index: 2; scale: 0.15; bottom: 450px; left: -400px; rotate: 190deg"
        />

        <img
            transition:fly={{x: -200, easing: cubicOut, duration: 1900}}
            src="/images/shapes/shape4.webp"
            alt=""
            style="--index: 3; scale: 0.25; bottom: 300px; left: -650px;"
        />
    </div>
{/if}

{#if scrollY < 270}
    <div id="collectionRight">
        <img
            transition:fly={{x: 200, easing: cubicOut, duration: 1800}}
            src="/images/shapes/shape1.webp"
            alt=""
            style="--index: 1; scale: 0.7; bottom: 200px; right: -350px;"
        />

        <img
            transition:fly={{x: 200, easing: cubicOut, duration: 2200}}
            src="/images/shapes/shape5.webp"
            alt=""
            style="--index: 0; scale: 0.3; bottom: 0px; right: -200px;"
        />

        <img
            transition:fly={{x: 200, easing: cubicOut, duration: 2200}}
            src="/images/shapes/shape4.webp"
            alt=""
            style="--index: 2; scale: 0.15; bottom: -40px; right: 50px;"
        />
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
    <img
        src="/images/animalBanner.webp"
        id="animalBanner"
        alt="Decorative banner featuring animal plushies"
    />

    {#if screenWidth > 750}
        <div aria-hidden="true" style:height=250px></div>
    {:else}
        <div aria-hidden="true" style:height=80px></div>
    {/if}

    <h2
        style:font-size=50px
        style:font-weight=900
        style:color="rgb(237, 233, 178)"
    >
        about
    </h2>

    <p>
        Build websites, games, and art about something toy-themed or cute.
        <strong>Get plushies, lamps, merch, and more!</strong>
    </p>

    <div style="display: block; width: 90%; height: 300px; margin: {screenWidth > 750 ? '100px' : '80px'} auto 100px auto;">
        <div id="prizeCarousel" aria-hidden="true">
            <img alt="" src="/images/shapes/shape3.webp" style:user-select="none"/>

            {#each displayList as itemName}
                {@const isMerch = itemName.includes("shirt") || itemName.includes("hoodie") || itemName.includes("sweatshirt")}

                <img
                    class="item"
                    src="/images/items/{itemName}.webp"
                    alt=""
                    style:opacity={currDisplay === itemName ? "1" : "0"}
                    style:pointer-events={currDisplay === itemName ? "auto" : "none"}
                    style:transform="translate(-50%, -50%) rotate({isMerch ? 5 : 0}deg)"
                    aria-hidden={currDisplay === itemName ? "false" : "true"}
                    translate="no"
                />
            {/each}
        </div>
    </div>

    <p>
        Earn tokens from each project you build and ship. Use those tokens to
        purchase <strong>crates</strong>, which unlock random prizes from its category.
    </p>

    <div
        style:margin-top=-30px
        style:margin-bottom=-20px;
        id="landingCrates"
        aria-label="A token, alongside examples of prize crates"
        style:flex-direction={screenWidth > 750 ? "row" : "column"}
    >
        <div style:margin-top={screenWidth > 750 ? 0 : 50}px>
            <img
                src="/images/tokenArrow{screenWidth > 750 ? "" : "_mobile"}.webp"
                style:max-height=400px
                style:animation="pulseShape 3s infinite ease-in-out"
                id="landingCrates"
                alt=""
                translate="no"
            />
        </div>

        <div class="crateContainer">
            <div class="crate crateIkea">
                <img
                    src="/images/crates/ikea.webp"
                    alt=""
                />
            </div>

            <div class="crate crateHoodies">
                <img
                    src="/images/crates/hoodies.webp"
                    alt=""
                />
            </div>
        </div>
    </div>
    <h3 style:font-size=35px style:font-weight=900 style:margin-top=-150px;>what can I build?</h3>
    <p>Any software project, from games to websites, that meets the theme! The best projects also typically include original art.</p>
    <div id="ideas">
         <div style:width={screenWidth > 750 ? 50 : 100}% id="ideaSide">
            <div>A lofi-app with cute scenery and art</div>
            <div>A game where an angry goose chases you</div>
            <div>A website about all the plushies you own</div>
            <div>A virtual pet</div>
         </div>
         <div style:display={screenWidth > 750 ? "block" : "none"} style="width: 50%">
            <img src="/images/aftonsparv.webp" alt="Alien plushie" />
         </div>
    </div>
</div>
