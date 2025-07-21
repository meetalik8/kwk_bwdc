<script>
  import { onMount } from "svelte";
  
  let { children, callback, options } = $props();
  
  // this uniqueId just lets us target the element
  // with `document.getElementById(uniqueId)` later on.
  // it's a little hacky, but it works.
  let uniqueId = Math.random().toString();
  
  // here we define the onMount() function for this component.
  // svelte handles calling the onMount() function *after* all of the HTML in this
  // component has been mounted to the DOM. we have to put the intersection observer
  // stuff in onMount() because we need to target the <div> we create below,
  // but it won't actually exist in the DOM until it's been mounted.
  onMount(() => {
    let intersectionObserver = new IntersectionObserver(callback, options);
    
    const observedElement = document.getElementById(uniqueId);
    intersectionObserver.observe(observedElement);
  });
</script>

<!-- assign the containing div the id `uniqueId` so we can target it -->
<div id={uniqueId} class="article-text">
  <div class="content">
    {@render children()}
  </div>
</div>

<style>
  .article-text {
    margin: 50vh auto;
    width: 70%;
    background: white;
    color: #1e293b;
    border: 1px solid rgba(226, 232, 240, 0.8);
    border-radius: 16px;
    padding: 2.5rem;
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 4px 6px -1px rgba(0, 0, 0, 0.06);
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    backdrop-filter: blur(10px);
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    position: relative;
    overflow: hidden;
  }

  .article-text::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: linear-gradient(90deg, #3b82f6, #06b6d4);
    transform: translateX(-100%);
    transition: transform 0.4s ease;
  }

  .article-text:hover::before {
    transform: translateX(0);
  }

  .article-text:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  }

  .content {
    position: relative;
    z-index: 1;
  }

  :global(.article-text h2) {
    color: #1e293b;
    font-weight: 700;
    margin-bottom: 1.5rem;
    font-size: 1.8rem;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    letter-spacing: -0.02em;
  }

  :global(.article-text p) {
    color: #475569;
    font-size: 1.1rem;
    line-height: 1.7;
    margin: 0;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    font-weight: 400;
  }
  @media (max-width: 768px) {
    .article-text {
      width: 85%;
      padding: 2rem;
      margin: 40vh auto;
    }

    :global(.article-text h2) {
      font-size: 1.6rem;
    }

    :global(.article-text p) {
      font-size: 1rem;
    }
  }

  @media (max-width: 480px) {
    .article-text {
      width: 90%;
      padding: 1.5rem;
    }

    :global(.article-text h2) {
      font-size: 1.4rem;
    }

    :global(.article-text p) {
      font-size: 0.95rem;
    }
  }
</style>