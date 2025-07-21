<script>
    let { children } = $props();
</script>

<div class="article-text">
    <div class="content">
        <div class="text-content">
            {@render children()}
        </div>
    </div>
</div>

<style>
    .article-text {
        margin: 50vh auto;
        width: 70%;
        background: #0072BB;
        color: #ffffff;
        border: 3px solid #8427c9;
        border-radius: 20px;
        padding: 2.5rem;
        box-shadow: 16px 16px 0px #8a8a8a;
        transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
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
        background: linear-gradient(90deg, #8427c9, #ffffff);
        transform: translateX(-100%);
        transition: transform 0.4s ease;
    }
    
    .article-text:hover::before {
        transform: translateX(0);
    }
    
    .article-text:hover {
        transform: translateY(-4px);
        box-shadow: 20px 20px 0px #8a8a8a;
    }
    
    .content {
        position: relative;
        z-index: 1;
    }
    
    .text-content {
        color: #e2e8f0;
        font-size: 1.2rem;
        line-height: 1.7;
        font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
        font-weight: 400;
    }
    
    
    @media (max-width: 768px) {
        .article-text {
            width: 85%;
            padding: 2rem;
            margin: 40vh auto;
        }
        .text-content {
            font-size: 1.1rem;
        }
    }
    
    @media (max-width: 480px) {
        .article-text {
            width: 90%;
            padding: 1.5rem;
        }
        .text-content {
            font-size: 1rem;
        }
    }
</style>