<script>
  import { onMount } from "svelte";

  const scrollTexts = [
    "Leadership is often seen as a reflection of merit and education.",
    "But representation in management still varies sharply across race and gender.",
    "White men dominate leadership, even in diverse counties like Fulton.",
    "Despite higher degrees, access doesn't always follow qualification.",
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

<div class="scroll-container">
  {#each scrollTexts as text, i}
    <section class="employment-scroll">
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

<section class="tldr-summary">
  <div class="tldr-container">
    <div class="tldr-header">
      <h2>TL;DR — What This Means</h2>
      <div class="header-accent"></div>
    </div>
    
    <div class="insights-grid">
      <div class="insight-card">
        <div class="insight-icon">👔</div>
        <p>In leadership roles, <strong>White men are significantly overrepresented</strong> in Georgia and Fulton County.</p>
      </div>
      
      <div class="insight-card">
        <div class="insight-icon">💪</div>
        <p><strong>Black women in Fulton</strong> hold more leadership roles than Black men, despite historic barriers.</p>
      </div>
      
      <div class="insight-card">
        <div class="insight-icon">🎓</div>
        <p><strong>Higher education helps</strong> — but doesn't guarantee equal leadership access for all races.</p>
      </div>
      
      <div class="insight-card">
        <div class="insight-icon">🔓</div>
        <p>The pathway from education to opportunity remains <strong>unequal</strong> — and leadership structures reflect that.</p>
      </div>
    </div>
    
    <div class="tldr-footer">
      <p class="footer-text">Understanding these patterns is the first step toward more equitable leadership representation.</p>
    </div>
  </div>
</section>

<style>
  .scroll-container {
    position: relative;
  }

  .employment-scroll {
    height: 100vh;
    position: relative;
    background-image: url('./public/mgmt.jpg'); 
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .overlay {
    background-color: rgba(0, 0, 0, 0.6);
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
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    font-weight: 600;
    font-size: 2rem;
    padding: 2rem;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
    line-height: 1.4;
  }

  .text-container.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .tldr-summary {
    background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
    padding: 5rem 2rem;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
  }

  .tldr-container {
    max-width: 1000px;
    margin: 0 auto;
  }

  .tldr-header {
    text-align: center;
    margin-bottom: 3rem;
  }

  .tldr-header h2 {
    font-size: 2.5rem;
    font-weight: 700;
    color: #1e293b;
    margin-bottom: 1rem;
    letter-spacing: -0.02em;
  }

  .header-accent {
    width: 80px;
    height: 4px;
    background: linear-gradient(90deg, #3b82f6, #06b6d4);
    margin: 0 auto;
    border-radius: 2px;
  }

  .insights-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
    margin-bottom: 3rem;
  }

  .insight-card {
    background: white;
    padding: 2rem;
    border-radius: 16px;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    border: 1px solid rgba(226, 232, 240, 0.8);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .insight-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: linear-gradient(90deg, #3b82f6, #06b6d4);
    transform: translateX(-100%);
    transition: transform 0.3s ease;
  }

  .insight-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  }

  .insight-card:hover::before {
    transform: translateX(0);
  }

  .insight-icon {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    display: block;
  }

  .insight-card p {
    font-size: 1.1rem;
    line-height: 1.6;
    color: #475569;
    margin: 0;
    font-weight: 400;
  }

  .insight-card strong {
    color: #1e293b;
    font-weight: 600;
  }

  .tldr-footer {
    text-align: center;
    padding-top: 2rem;
    border-top: 1px solid rgba(226, 232, 240, 0.8);
  }

  .footer-text {
    font-size: 1.2rem;
    color: #64748b;
    font-style: italic;
    font-weight: 400;
    margin: 0;
  }

  @media (max-width: 768px) {
    .text-container {
      font-size: 1.5rem;
      padding: 1rem;
      max-width: 90%;
    }
    
    .employment-scroll {
      background-attachment: scroll;
    }

    .tldr-summary {
      padding: 3rem 1rem;
    }

    .tldr-header h2 {
      font-size: 2rem;
    }

    .insights-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    .insight-card {
      padding: 1.5rem;
    }
  }

  @media (max-width: 480px) {
    .text-container {
      font-size: 1.2rem;
    }

    .tldr-header h2 {
      font-size: 1.8rem;
    }

    .insight-card p {
      font-size: 1rem;
    }
  }
</style>