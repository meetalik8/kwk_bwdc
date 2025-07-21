<script>
    import { fade } from "svelte/transition";
    import { onMount } from 'svelte';

    let scrollY = 0;
    let {title, subtitle} = $props();
    onMount(() => {
        const handleScroll = () => {
            scrollY = window.scrollY;
            const bg = document.querySelector('.title-card::before'); 
            const container = document.querySelector('.title-card');
            if (container) {
                const scale = 1 + Math.min(scrollY / 1000, 0.5); 
                container.style.setProperty('--zoom-scale', scale);
            }
        };

        window.addEventListener('scroll', handleScroll);
        return () => window.removeEventListener('scroll', handleScroll);
    });


</script>


<div class="title-card" transition:fade>
        <div class="content">
        <h1>{title}</h1>
        <p>{subtitle}</p>
    </div>
</div>

<style>

    .title-card {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 2rem;
    box-sizing: border-box;
    font-family: "Inter", sans-serif;
    position: relative;
    overflow: hidden;
    background-color: #c6c6be;
}

.title-card::before {
    content: "";
    position: absolute;
    inset: 0;
    background-image: url('./georgia.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    opacity: 0.3;
    z-index: 0;

    transform: scale(var(--zoom-scale, 1));
    transform-origin: right bottom;
    transition: transform 0.1s ease-out;
    will-change: transform;
}

    
    .content {
        max-width: 800px;
        background-color: rgba(70, 87, 82, 0.75);
        padding: 2rem;
        border: 6px solid #000000;
        border-radius: 2rem;
        box-shadow: 16px 16px #3a3d3c;
        position: relative;
        z-index: 1;
    }

    h1 {
    font-size: 3rem;
    margin: 0;
    color: #ffffff;
    text-shadow: 
        2px 2px 4px rgba(0, 0, 0, 0.8),
        -1px -1px 0 #000,
        1px -1px 0 #000,
        -1px 1px 0 #000,
        1px 1px 0 #000;
}

p {
    font-size: 1.3rem;
    color: #f7f5eb;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.7);
    margin-top: 1rem;
}


    @media (max-width: 600px) {
        h1 {
            font-size: 2.2rem;
        }

        p {
            font-size: 1.1rem;
        }
    }
</style>
