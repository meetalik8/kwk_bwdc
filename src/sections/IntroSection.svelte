<script>
  import { onMount } from "svelte";
  
  const scrollTexts = [
    "They say education is the key to success.",
    "A college degree… years of study, sleepless nights, and sometimes thousands in debt.",
    "But what if you did everything right... and the door still didn't open?",
    "Does having the same degree... mean having the same opportunity?"
  ];

  let visibleIndex = -1;
  let observers = [];

  function reveal(node, { threshold = 0.5, index }) {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          visibleIndex = index;
        }
      },
      {
        threshold,
        rootMargin: '-10% 0px -10% 0px'
      }
    );
    
    observer.observe(node);
    observers.push(observer);
    
    return {
      destroy() {
        observer.unobserve(node);
        observer.disconnect();
      }
    };
  }

  onMount(() => {
    return () => {
      observers.forEach(observer => observer.disconnect());
      observers = [];
    };
  });
</script>

<style>
  .scroll-container {
    position: relative;
  }

  section {
    height: 100vh;
    position: relative;
    background-image: url('/students.jpg');
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .overlay {
    background-color: rgba(0, 0, 0, 0.65);
    position: absolute;
    inset: 0;
    z-index: 1;
  }

  .text-container {
    z-index: 2;
    width: 100%;
    max-width: 800px;
    text-align: center;
    color: #fff;
    font-family: 'Georgia', serif;
    font-weight: bold;
    font-size: 2rem;
    padding: 2rem;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .text-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Add some visual enhancements */
  .text-container {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
    line-height: 1.4;
  }

  /* Responsive design */
  @media (max-width: 768px) {
    .text-container {
      font-size: 1.5rem;
      padding: 1rem;
      max-width: 90%;
    }
  }

  @media (max-width: 480px) {
    .text-container {
      font-size: 1.2rem;
    }
  }

  /* Fix background attachment on mobile */
  @media (max-width: 768px) {
    section {
      background-attachment: scroll;
    }
  }
</style>

<div class="scroll-container">
  {#each scrollTexts as text, i}
    <section>
      <div class="overlay"></div>
      <div
        class="text-container"
        class:visible={visibleIndex === i}
        use:reveal={{ threshold: 0.5, index: i }}
      >
        {text}
      </div>
    </section>
  {/each}
</div>