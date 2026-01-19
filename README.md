# Forge — Portfolio Hero Component

## Overview

Forge is a sophisticated, split-panel hero component designed for personal portfolios, creative agencies, and designer showcases. Featuring a distinctive black-and-white aesthetic with bold typography and strategic use of color accents, this component creates immediate visual impact while maintaining clarity and purpose.

<img width="1920" height="1047" alt="forge" src="https://github.com/user-attachments/assets/5cdd9c89-282d-42aa-b3c4-a4e096b3dbcf" />

## Live Deployment

[View Demo](https://lefajmofokeng.github.io/Forge)  

---

## Technology Specifications

### Core Stack
- **HTML5**: Semantic markup with accessibility features
- **CSS3**: Flexbox layout, CSS custom properties, responsive design
- **No JavaScript**: Pure CSS implementation
- **Google Fonts**: Inter font family (400-900 weights)
- **Unsplash API**: High-quality professional imagery
- **SVG Icons**: Custom arrow icon for CTA button

### Design System
- **Color Palette**: Monochrome foundation with orange accent (#FF5D17)
- **Typography**: Inter font with strong weight hierarchy (700-900)
- **Layout**: Flexbox-based split panel with controlled aspect ratios
- **Visual Effects**: Grayscale filter, subtle hover animations
- **Spacing System**: Consistent padding and margin scale

---

## Architecture

### File Structure
```
forge/
├── index.html          # Semantic HTML with image fallback
├── style.css           # CSS Flexbox, variables, responsive design
└── README.md
```

### CSS Architecture
- **CSS Custom Properties**: Comprehensive theming system
- **Flexbox Layout**: Side-by-side desktop, stacked mobile
- **Aspect Ratio Control**: Modern `aspect-ratio` property with fallbacks
- **Mobile-first responsive**: Progressive enhancement approach
- **BEM-inspired naming**: Clear, maintainable class structure
- **Transitions**: Smooth hover and interaction states

### Image Strategy
1. **Unsplash CDN**: Professional, high-resolution images
2. **Grayscale filter**: Creates cohesive aesthetic
3. **Object-fit cover**: Consistent cropping across devices
4. **Fallback system**: Placeholder on load failure
5. **Fixed aspect ratio**: Maintains layout integrity

---

## Integration Guide

### Basic Implementation
```html
<!-- Add to head -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">

<!-- Add to body -->
<link rel="stylesheet" href="path/to/forge/style.css">
```

### Content Management System Integration

#### WordPress (PHP Template)
```php
<section class="hero-section-container">
    <div class="hero-content-block">
        <div class="visual-presentation-area">
            <?php 
            $hero_image = get_field('hero_image'); // ACF field
            if ($hero_image) : ?>
                <img 
                    src="<?php echo esc_url($hero_image['url']); ?>" 
                    class="hero-main-image" 
                    alt="<?php echo esc_attr($hero_image['alt']); ?>"
                    onerror="this.src='<?php echo get_template_directory_uri(); ?>/assets/fallback-hero.jpg'"
                >
            <?php else : ?>
                <img 
                    src="https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85" 
                    class="hero-main-image" 
                    alt="Default hero image"
                >
            <?php endif; ?>
        </div>
        
        <div class="call-to-action-area">
            <h1 class="headline-main">
                <?php echo get_field('hero_headline', 'option') ?: 'Crafting Meaningful Brands'; ?>
            </h1>
            
            <p class="description-lead">
                <?php echo get_field('hero_description', 'option') ?: 'Default description text.'; ?>
            </p>
            
            <a href="<?php echo get_field('hero_cta_link', 'option') ?: '#works'; ?>" class="cta-action-button">
                <svg class="button-icon-arrow" viewBox="0 0 24 24" stroke="currentColor">
                    <path d="M5 12h14"></path>
                    <path d="m12 5 7 7-7 7"></path>
                </svg>
                <?php echo get_field('hero_cta_text', 'option') ?: 'See my works'; ?>
            </a>
        </div>
    </div>
</section>
```

#### React/Next.js Component
```jsx
import './forge.css';

export default function ForgeHero({ 
  imageSrc, 
  altText, 
  headline, 
  description, 
  ctaText = 'See my works',
  ctaLink = '#works' 
}) {
  return (
    <div className="hero-section-container">
      <section className="hero-content-block">
        <div className="visual-presentation-area">
          <img 
            src={imageSrc || "https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85"}
            className="hero-main-image" 
            alt={altText || "Professional designer at work"}
            loading="eager"
            decoding="sync"
          />
        </div>
        
        <div className="call-to-action-area">
          <h1 className="headline-main">
            {headline || "Crafting Meaningful Brands & Intuitive Digital Experiences That Stand Out"}
          </h1>
          
          <p className="description-lead">
            {description || "I'm Lefa, a South African-based Brand and UI/UX Designer passionate about crafting visually compelling identities and seamless digital experiences."}
          </p>
          
          <a href={ctaLink} className="cta-action-button">
            <svg className="button-icon-arrow" viewBox="0 0 24 24" stroke="currentColor">
              <path d="M5 12h14"></path>
              <path d="m12 5 7 7-7 7"></path>
            </svg>
            {ctaText}
          </a>
        </div>
      </section>
    </div>
  );
}
```

#### Vue.js Component
```vue
<template>
  <div class="hero-section-container">
    <section class="hero-content-block">
      <div class="visual-presentation-area">
        <img 
          :src="imageSrc" 
          :alt="altText"
          class="hero-main-image"
          @error="handleImageError"
          loading="eager"
        />
      </div>
      
      <div class="call-to-action-area">
        <h1 class="headline-main">{{ headline }}</h1>
        <p class="description-lead">{{ description }}</p>
        <a :href="ctaLink" class="cta-action-button">
          <svg class="button-icon-arrow" viewBox="0 0 24 24" stroke="currentColor">
            <path d="M5 12h14"></path>
            <path d="m12 5 7 7-7 7"></path>
          </svg>
          {{ ctaText }}
        </a>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import './forge.css';

const props = defineProps({
  imageSrc: {
    type: String,
    default: 'https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85'
  },
  altText: {
    type: String,
    default: 'Professional designer at work'
  },
  headline: {
    type: String,
    default: 'Crafting Meaningful Brands & Intuitive Digital Experiences That Stand Out'
  },
  description: {
    type: String,
    default: "I'm Lefa, a South African-based Brand and UI/UX Designer passionate about crafting visually compelling identities and seamless digital experiences."
  },
  ctaText: {
    type: String,
    default: 'See my works'
  },
  ctaLink: {
    type: String,
    default: '#works'
  }
});

const handleImageError = (e) => {
  e.target.src = 'https://placehold.co/1000x1100/333/fff?text=Image+Error';
};
</script>
```

---

## Customization

### Theming System
Modify CSS variables for brand alignment:
```css
:root {
    --color-dark-bg: #0a0a0a; /* Softer black */
    --color-content-bg: #111111; /* Dark gray background */
    --color-text-primary: #f5f5f5; /* Off-white text */
    --color-text-secondary: #a0a0a0; /* Muted gray */
    --color-cta-orange: #FF6B35; /* Custom accent color */
    --color-cta-hover: #FF8C5A; /* Hover state */
    --border-radius-large: 8px; /* Rounded corners */
    --font-inter: 'Inter', sans-serif;
    --max-width-desktop: 1400px; /* Wider container */
    --content-gap: 4rem; /* Increased spacing */
}
```

### Layout Configuration
Adjust component proportions:
```css
.hero-content-block {
    gap: 4rem; /* Increase spacing between image and text */
    max-height: 700px; /* Taller hero section */
}

.visual-presentation-area {
    flex: 1; /* Equal width with text area */
    aspect-ratio: 4/5; /* Portrait orientation */
}

.call-to-action-area {
    flex: 1; /* Equal width with image area */
    padding: 4rem; /* More breathing room */
}
```

### Typography Scale
Customize text hierarchy:
```css
.headline-main {
    font-size: 4rem; /* Larger headline */
    font-weight: 800; /* Extra bold */
    line-height: 1.1;
    letter-spacing: -0.04em;
}

.description-lead {
    font-size: 1.5rem; /* Larger body text */
    line-height: 1.7;
    font-weight: 500; /* Medium weight */
}
```

### Interactive States
Enhance user feedback:
```css
.cta-action-button {
    padding: 1rem 2.5rem;
    font-size: 1.1rem;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
}

.cta-action-button:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(255, 93, 23, 0.3);
}

.cta-action-button:active {
    transform: translateY(-1px);
}

.cta-action-button::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 5px;
    height: 5px;
    background: rgba(255, 255, 255, 0.5);
    opacity: 0;
    border-radius: 100%;
    transform: scale(1, 1) translate(-50%, -50%);
    transform-origin: 50% 50%;
}

.cta-action-button:focus:not(:active)::after {
    animation: ripple 1s ease-out;
}

@keyframes ripple {
    0% {
        transform: scale(0, 0);
        opacity: 0.5;
    }
    100% {
        transform: scale(40, 40);
        opacity: 0;
    }
}
```

---

## Advanced Features

### Dark/Light Mode Toggle
Add theme switching capability:
```css
:root[data-theme="light"] {
    --color-dark-bg: #f8f9fa;
    --color-content-bg: #ffffff;
    --color-text-primary: #212529;
    --color-text-secondary: #495057;
    --color-cta-orange: #e8590c;
}

@media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) {
        /* Default dark theme */
    }
}
```

### Parallax Scroll Effect
Add subtle depth with CSS:
```css
.visual-presentation-area {
    transform: translateZ(0);
    will-change: transform;
}

@media (prefers-reduced-motion: no-preference) {
    .hero-section-container {
        overflow: hidden;
    }
    
    .visual-presentation-area {
        transition: transform 0.3s ease-out;
    }
    
    .hero-section-container:hover .visual-presentation-area {
        transform: translateY(-10px);
    }
}
```

### Performance Optimizations

#### Image Optimization
```html
<img 
    src="image.jpg" 
    srcset="image-400.jpg 400w, image-800.jpg 800w, image-1200.jpg 1200w"
    sizes="(max-width: 600px) 100vw, (max-width: 1024px) 50vw, 40vw"
    alt="Description"
    class="hero-main-image"
    loading="eager"
    decoding="sync"
    width="1000"
    height="1100"
>
```

#### Critical CSS Inlining
```html
<style>
.hero-section-container {
    opacity: 0;
    animation: fadeIn 0.5s ease-out forwards;
}

@keyframes fadeIn {
    to { opacity: 1; }
}

/* Above-the-fold styles only */
</style>
```

#### Font Loading Strategy
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
<noscript>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
</noscript>
```

---

## Accessibility Compliance

### WCAG 2.1 AA Standards
- **Semantic HTML**: Proper heading hierarchy and landmark roles
- **Keyboard navigation**: All interactive elements accessible
- **Focus indicators**: Visible focus states
- **Color contrast**: Minimum 4.5:1 ratio (tested)
- **Screen reader support**: Descriptive alt text and aria labels
- **Reduced motion support**: Respects `prefers-reduced-motion`

### Enhanced Accessibility Features
```css
.cta-action-button:focus {
    outline: 3px solid var(--color-cta-orange);
    outline-offset: 3px;
}

@media (prefers-reduced-motion: reduce) {
    .cta-action-button,
    .hero-main-image {
        transition: none;
    }
}

.hero-main-image {
    /* Provide context for screen readers */
    aria-describedby="image-description";
}
```

---

## Browser Support

| Browser | Version | Support | Notes |
|---------|---------|---------|-------|
| Chrome  | 60+     | Full    | Optimal performance |
| Firefox | 55+     | Full    | CSS aspect-ratio support |
| Safari  | 14+     | Full    | Requires prefix for some features |
| Edge    | 79+     | Full    | Chromium-based version |
| Mobile  | iOS 14+/Android 9+ | Full | Touch-optimized |

### Fallback for Older Browsers
```css
.visual-presentation-area {
    /* Modern aspect-ratio with fallback */
    aspect-ratio: 1 / 1.1;
    height: 0;
    padding-bottom: 110%; /* 1/1.1 aspect ratio fallback */
}

@supports (aspect-ratio: 1 / 1.1) {
    .visual-presentation-area {
        height: auto;
        padding-bottom: 0;
    }
}
```

---

## SEO Optimization

### Best Practices
1. **Semantic markup**: Proper use of headings and sections
2. **Structured data ready**: Person/Portfolio schema can be added
3. **Image optimization**: Alt text, dimensions, and loading strategy
4. **Performance**: Fast loading impacts SEO positively

### Portfolio Schema Implementation
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Lefa Mofokeng",
  "jobTitle": "Brand and UI/UX Designer",
  "url": "https://yourportfolio.com",
  "sameAs": [
    "https://github.com/thisislefa"
  ],
  "knowsAbout": ["Brand Design", "UI/UX Design", "Digital Experiences"],
  "description": "South African-based Brand and UI/UX Designer passionate about crafting visually compelling identities and seamless digital experiences.",
  "image": "https://images.unsplash.com/photo-1494438639946-1ebd1d20bf85"
}
</script>
```

---

## Troubleshooting

### Common Issues and Solutions

#### Image Loading Problems
**Issue**: Image fails to load or shows incorrectly.
**Solution**: Implement robust fallback system:
```javascript
// Additional JavaScript fallback
document.querySelectorAll('.hero-main-image').forEach(img => {
    img.addEventListener('error', function() {
        if (!this.getAttribute('data-fallback-used')) {
            this.src = 'https://placehold.co/1000x1100/222/fff?text=Designer+Portfolio';
            this.setAttribute('data-fallback-used', 'true');
        }
    });
});
```

#### Layout Shifting on Mobile
**Issue**: Content jumps during page load.
**Solution**: Reserve space with CSS:
```css
.visual-presentation-area {
    min-height: 400px; /* Reserve space */
    background: linear-gradient(45deg, #222, #333); /* Loading gradient */
}

.hero-main-image {
    opacity: 0;
    transition: opacity 0.3s ease;
}

.hero-main-image.loaded {
    opacity: 1;
}
```

#### Font Loading FOUT
**Issue**: Flash of unstyled text during font load.
**Solution**: Implement font-display strategy:
```css
@font-face {
    font-family: 'Inter';
    font-style: normal;
    font-weight: 400 900;
    font-display: swap;
    src: url('path/to/inter.woff2') format('woff2');
}
```

#### Button Contrast Issues
**Issue**: CTA button doesn't meet contrast requirements.
**Solution**: Adjust colors for compliance:
```css
.cta-action-button {
    background-color: #D84315; /* Darker orange for contrast */
    color: #FFFFFF;
}

.cta-action-button:hover {
    background-color: #E64A19;
}
```

---

## Performance Monitoring

### Core Web Vitals Targets
- **LCP (Largest Contentful Paint)**: Hero image should load within 2.5s
- **CLS (Cumulative Layout Shift)**: <0.1 (stable layout)
- **FID (First Input Delay)**: <100ms (responsive CTA button)

### Optimization Checklist
- [ ] **Image compression**: WebP format with JPEG fallback
- [ ] **Font subsetting**: Include only necessary weights
- [ ] **Critical CSS**: Inline above-the-fold styles
- [ ] **Lazy loading**: Defer non-critical resources
- [ ] **Cache strategy**: Leverage browser caching for assets

---

## Maintenance

### Regular Updates
1. **Content refresh**: Update headline and description quarterly
2. **Image rotation**: Change hero image seasonally
3. **Performance audit**: Quarterly Lighthouse testing
4. **Browser testing**: Test on new browser versions

### Version History
- **v1.0**: Initial release with split-panel design
- **v1.1**: Added responsive improvements
- **v1.2**: Enhanced accessibility and performance
- **v1.3**: Added advanced customization options

---

## License

[MIT License](https://github.com/thisislefa/BrandCraft/blob/main/LICENSE) — Free for personal and commercial use with attribution.

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -m 'Add enhancement'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

---

## Support

For technical issues:
1. Check the troubleshooting section
2. Test with browser developer tools
3. Open an issue with specific details

---

**Forge** — A distinctive hero component for modern creative portfolios.






