# Cartzy 🛒

A modern e-commerce web application built with **React** — featuring dark/light theme, smooth animations, Clerk authentication, EmailJS contact form, and fully responsive design. Currently being upgraded with **Next.js**, **TypeScript**, and a professional backend setup.

🔗 **Live:** [https://ecommerce-site-roan-gamma.vercel.app](https://ecommerce-site-roan-gamma.vercel.app)  
💻 **Repository:** [https://github.com/anjumhere/Ecommerce-website-react](https://github.com/anjumhere/Ecommerce-website-react)

---

## 🚀 Tech Stack

### Frontend (Current)
| Technology | Purpose |
| --- | --- |
| React 18 | UI framework |
| React Router DOM v6 | Client-side routing |
| Tailwind CSS v4 | Styling & responsive design |
| Swiper.js | Hero carousel |
| Clerk | Authentication |
| EmailJS | Contact form emails |
| Axios | HTTP requests |
| Lucide React + React Icons | Icon library |
| Vercel | Deployment |

### Backend (In Progress)
| Technology | Purpose |
| --- | --- |
| **Next.js 14+** | Full-stack framework (upcoming) |
| **TypeScript** | Type-safe code |
| **Node.js** | Runtime |
| **Express.js** | Backend framework |
| **MongoDB** | Database |
| **Mongoose** | ODM (Object Data Modeling) |

### Additional Tools
| Tool | Purpose |
| --- | --- |
| Nominatim (OpenStreetMap) | Reverse geocoding for location |

---

## 📁 Project Structure

```
cartzy/
├── public/
├── src/
│   ├── assets/
│   │   └── banner.jpg
│   ├── components/
│   │   ├── Navbar.jsx        # Sticky navbar, mobile drawer, theme toggle
│   │   ├── Carousel.jsx      # Hero slider with floating product images
│   │   ├── Category.jsx      # Infinite marquee of categories
│   │   ├── FeaturesSection.jsx
│   │   ├── MidBanner.jsx     # Parallax banner
│   │   └── Footer.jsx
│   ├── context/
│   │   └── DataContext.jsx   # Global state (to be replaced with API calls)
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Products.jsx      # Grid with sidebar filters
│   │   ├── Cart.jsx          # Cart + order summary
│   │   ├── About.jsx
│   │   ├── Contact.jsx       # Working EmailJS form
│   │   └── SignIn.jsx
│   ├── App.jsx               # Router + theme state + location logic
│   ├── main.jsx              # Entry — ClerkProvider + DataProvider
│   └── index.css
├── .env                      # Environment variables (local)
├── .gitignore
├── README.md
├── vercel.json               # Vercel deployment config
├── vite.config.js            # Vite build config
└── package.json
```

---

## ✨ Features

### Hero Carousel
- Built with **Swiper.js**, autoplay every 4 seconds
- 5 dark slides with unique accent colors
- Product image floats with `floatY` CSS keyframe animation
- Ambient glow blob + colored drop-shadow
- Responsive: column layout on mobile, side-by-side on desktop
- Custom `useIsMobile` hook to override Swiper's flex behavior

### Category Marquee
- Infinite scrolling ticker of 10 product categories
- Seamless loop with duplicated array
- Pauses on hover
- Pastel color scheme for each chip

### Products Page
- **Category filter** — matches against `product.category`
- **Price filter** — multiple thresholds ($100, $200, $400, $500, $1000, $1200)
- **Clear Filters** button (appears when filters active)
- Collapsible category list
- Mobile: filters hidden behind toggle button
- Product cards with hover lift, discount badge, word-limited titles

### Shopping Cart
- Quantity controls (+ / −) with `updateQuantity`
- Remove item via `removeFromCart`
- **Subtotal** = sum of `price × quantity`
- **Shipping** = $15 flat, FREE if subtotal > $100
- "Add $X more for free shipping" nudge
- Promo code input field
- Checkout stepper: Cart → Shipping → Payment
- Empty cart state with CTA

### Authentication (Clerk)
- Sign In / Sign Out via Clerk hosted UI
- Conditional rendering with `<Show when="signed-in/out">`
- UserButton avatar displayed when signed in

### Contact Form (EmailJS)
- Real emails sent directly to Gmail (no backend required)
- Inquiry type selector (General inquiry / Product Support)
- Loading state ("Sending...") while submitting
- Success screen after message sent
- Error handling & validation

### Theme System
- Light/Dark mode toggle (☀️ / 🌙)
- Theme state passed to all components
- Consistent styling across light & dark themes

### Location Detection
- "Add Address" pill in Navbar
- Uses `navigator.geolocation` API
- Reverse geocoded via Nominatim
- Displays county + state information

### Responsive Design
- **Desktop:** Full navigation, location, theme, cart, sign in
- **Mobile:** Hamburger menu with drawer
- Cart badge shows item count
- Mobile-first approach throughout

### Parallax Animation
- Custom JS parallax via `useRef` + scroll listener
- `backgroundPositionY` shifts at 0.2× scroll speed
- Works on iOS Safari (unlike `background-attachment: fixed`)

---

## 🐛 Bugs Fixed

| Component | Bug | Fix |
| --- | --- | --- |
| Cart.jsx | `acc * item.price` (multiplication bug) | Changed to `acc + item.price * item.quantity` |
| Cart.jsx | Empty Order Summary `<div>` | Built complete summary panel |
| FeaturesSection.jsx | All 4 features labeled "Free Shipping" | Each now has correct label & description |
| Products.jsx | Filter matched `product.description` | Fixed to match `product.category` |
| MidBanner.jsx | `background-attachment: fixed` broken on iOS | Replaced with JS scroll parallax |
| Contact.jsx | Off-brand `ring-blue-500` | Changed to `ring-red-400` |
| Carousel.jsx | Tailwind flex ignored by Swiper | Switched to inline styles + `useIsMobile` |
| Navbar.jsx | No mobile menu | Added hamburger + drawer navigation |

---

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/anjumhere/Ecommerce-website-react.git
cd Ecommerce-website-react

# Install dependencies
npm install

# Create .env file
echo "VITE_CLERK_PUBLISHABLE_KEY=your_key_here" > .env

# Get your Clerk key from dashboard.clerk.com

# Start development server
npm run dev
```

---

## 🔐 Environment Variables

| Variable | Source | Required |
| --- | --- | --- |
| `VITE_CLERK_PUBLISHABLE_KEY` | [dashboard.clerk.com](https://dashboard.clerk.com) → API Keys | ✅ Yes |

> **Note:** EmailJS credentials are handled directly in `Contact.jsx` — the public key is safe to expose in frontend code by design.

---

## 🌐 Deployment

Currently deployed on **Vercel**. To deploy your own:

1. Push to GitHub
2. Import repository on [vercel.com](https://vercel.com)
3. Add environment variables under Settings → Environment Variables
4. Deploy

```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

---

## 🛣️ Routes

| Path | Page | Description |
| --- | --- | --- |
| `/` | Home | Carousel, features section, banner |
| `/products` | Products | Grid with category & price filters |
| `/cart` | Cart | Cart items + order summary |
| `/about` | About | Brand story, stats, team info |
| `/contact` | Contact | EmailJS contact form |
| `/signin` | Sign In | Clerk authentication page |

---

## 🎨 Design System

### Carousel Accent Colors

| Slide | Background | Accent Color |
| --- | --- | --- |
| 1 | `#0a0a0a` | 🟠 `#ff6b35` Orange |
| 2 | `#060d18` | 🔵 `#3b82f6` Blue |
| 3 | `#08060f` | 💜 `#a855f7` Purple |
| 4 | `#06100a` | 🟢 `#22c55e` Green |
| 5 | `#100808` | 🌹 `#f43f5e` Rose |

### Key Animations

| Animation | Location | Duration |
| --- | --- | --- |
| `floatY` | Carousel product image | 5s infinite |
| `scroll` | Category marquee | 35s infinite |
| `scrollPulse` | About hero section | 1.8s infinite |
| FadeIn | About page sections | 0.6s on scroll |

---

## 🚧 Roadmap (In Progress)

### Phase 1: TypeScript Migration
- [ ] Convert components to TypeScript
- [ ] Type-safe context & state management
- [ ] Proper interface definitions for products, cart, orders

### Phase 2: Next.js Upgrade
- [ ] Migrate from Vite + React Router to Next.js App Router
- [ ] API routes for backend integration
- [ ] Server-side rendering (SSR) for better SEO
- [ ] Static generation for product pages

### Phase 3: Backend Integration
- [ ] Express.js API server (separate or Next.js API routes)
- [ ] MongoDB database for products, users, orders
- [ ] Authentication with JWT + Clerk sync
- [ ] Cart persistence to database
- [ ] Order management system
- [ ] Payment processing integration (Stripe/PayPal)

### Phase 4: Production Setup
- [ ] Environment configuration for staging/production
- [ ] Error handling
- [ ] Error handling & validation
- [ ] Performance monitoring
- [ ] Security best practices
- [ ] API rate limiting & validation
- [ ] Database indexing & optimization

---

## 🛠️ Getting Started with Backend Integration

### Prerequisites
```bash
Node.js 16+ 
npm or yarn
MongoDB Atlas account (free tier available)
```

### Backend Setup (Upcoming)
```bash
# Create backend directory
mkdir cartzy-backend
cd cartzy-backend

# Initialize Node.js project
npm init -y

# Install dependencies
npm install express mongoose cors dotenv axios
npm install -D typescript ts-node @types/node nodemon
```

### Example API Endpoint Structure
```typescript
// routes/products.ts
import { Router } from 'express';
import ProductController from '../controllers/productController';

const router = Router();

router.get('/', ProductController.getAllProducts);
router.get('/:id', ProductController.getProductById);
router.post('/', ProductController.createProduct);
router.put('/:id', ProductController.updateProduct);
router.delete('/:id', ProductController.deleteProduct);

export default router;
```

---

## 📚 Learning Resources

### TypeScript
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [TypeScript for React Developers](https://www.typescriptlang.org/docs/handbook/react.html)

### Next.js
- [Next.js Official Docs](https://nextjs.org/docs)
- [Next.js App Router Guide](https://nextjs.org/docs/app)
- [Next.js API Routes](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)

### Backend Development
- [Express.js Guide](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Mongoose ODM](https://mongoosejs.com/)

### Full-Stack Resources
- [MERN Stack Tutorial](https://www.mern.io/)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

---

## 🎯 Development Workflow

### Local Development
```bash
# Terminal 1: Frontend (React/Vite)
npm run dev

# Terminal 2: Backend (Node/Express) - Coming soon
npm run server

# Terminal 3: Watch TypeScript
npm run watch
```

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/cart-api

# Make changes and commit
git add .
git commit -m "feat: implement cart API endpoints"

# Push and create PR
git push origin feature/cart-api
```

### Code Quality
```bash
# Format code with Prettier
npm run format

# Lint with ESLint
npm run lint

# Run tests (when added)
npm run test
```

---

## 🔐 Security Best Practices

- ✅ Keep API keys in `.env` files (never commit)
- ✅ Use HTTPS for all API calls
- ✅ Validate & sanitize user inputs
- ✅ Implement CORS properly
- ✅ Use JWT for authentication
- ✅ Hash passwords with bcrypt
- ✅ Rate limit API endpoints
- ✅ Add request validation middleware
- ✅ Use environment-specific configs

---

## 🚀 Deployment Strategy

### Frontend (Vercel) - Current
- Automatic deployments from GitHub
- Edge functions for serverless logic
- Preview deployments for PRs

### Backend (Recommended Platforms)
- **Railway.app** — Easy Next.js deployment
- **Render.com** — Free tier for Node.js
- **Fly.io** — Great for full-stack apps
- **Vercel** — Native Next.js API Routes support

### Database (MongoDB Atlas)
- Free M0 cluster tier
- Automatic backups
- Horizontal scaling ready

---

## 📊 Project Metrics

| Metric | Value |
| --- | --- |
| **Codebase** | React 18 + React Router |
| **Styling** | Tailwind CSS v4 |
| **State Management** | Context API (→ Redux planned) |
| **Authentication** | Clerk + JWT (planned) |
| **API Communication** | Axios + REST (→ GraphQL planned) |
| **Performance** | Optimized component rendering |
| **Accessibility** | WCAG 2.1 AA compliant |
| **Mobile Score** | Excellent (responsive design) |

---

## 💡 Tips for Success

1. **Start Small** — Build API endpoints one at a time
2. **Test Early** — Write tests for critical functions
3. **Document Code** — Use JSDoc/TSDoc comments
4. **Use Types** — TypeScript catches errors early
5. **Version Control** — Commit frequently with clear messages
6. **Code Review** — Ask for feedback on your PRs
7. **Monitor Performance** — Use DevTools & profiling
8. **Stay Updated** — Keep dependencies current

---

## 🤝 Contributing

This is a personal learning project, but contributions and suggestions are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ❓ FAQ

**Q: When will the backend be added?**  
A: I'm learning Node.js, Express, and MongoDB now. Backend integration is planned for Q2 2026.

**Q: Can I use this as a template?**  
A: Yes! Feel free to fork and customize for your own e-commerce project.

**Q: What payment system will be used?**  
A: Planning to integrate Stripe or PayPal in Phase 3.

**Q: Is this production-ready?**  
A: Currently in development. Great for learning and portfolio projects!

---

## 👨‍💻 About the Developer

**Adnan Anjum** — Passionate Full-Stack Developer in Training

- 🌍 **Location:** Islamabad, Pakistan 🇵🇸
- 📚 **Currently Learning:** Next.js 14+ | TypeScript | Node.js + Express | MongoDB
- 🎯 **Goal:** Build production-ready full-stack MERN applications
- 💻 **GitHub:** [@anjumhere](https://github.com/anjumhere)
- 📧 **Email:** [anjumcode12@gmail.com](mailto:anjumcode12@gmail.com)
- 🔗 **LinkedIn:** [Adnan Anjum](https://www.linkedin.com/in/adnan-anjum-196a373a1/)

### Current Skills
```
Frontend:  React ████████░░ 80% | TypeScript ██░░░░░░░░ 20%
Backend:   Node.js ███░░░░░░░ 30% | Express ███░░░░░░░ 30%
Database:  MongoDB ███░░░░░░░ 30% | Mongoose ███░░░░░░░ 30%
Tools:     Git ████████░░ 80% | Vercel ██████░░░░ 60%
```

### Learning Milestones
- ✅ React Fundamentals (Hooks, State, Props)
- ✅ React Router DOM Navigation
- ✅ Tailwind CSS Styling
- ✅ API Integration (Axios)
- ⏳ TypeScript Deep Dive (In Progress)
- ⏳ Next.js App Router (In Progress)
- 📋 Express.js Backend (Coming Soon)
- 📋 MongoDB Database (Coming Soon)
- 📋 Full-Stack MERN (Q3 2026 Target)

---

## 📜 License

MIT License — Feel free to use this project for learning and building awesome things!

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

---

<div align="center">

## ⭐ Support This Project

If you find this project helpful, please consider:

- ⭐ **Starring** this repository
- 🔗 **Sharing** with others learning web development
- 💬 **Providing feedback** and suggestions
- 🤝 **Contributing** with improvements

<br>

### Made with 💻 and ☕ by Adnan Anjum

**"Code is poetry written in logic. Build something amazing!"** 🚀

</div>
