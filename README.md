# 🚀 Nuxt 4 Professional Template

A modern, production-ready **Nuxt 4 Starter Template** featuring best practices, premium components, and developer experience optimizations.

Created by [@akbarwebdev](https://github.com/AkbarshohIlhomovich) 💻

---

## ✨ Features

- ⚡ **Nuxt 4** - Latest version with enhanced performance
- 🎨 **Nuxt UI** - Beautiful components with Tailwind CSS integration
- 🗂 **Pinia** - Intuitive state management solution
- 🔗 **Vue Router** - Pre-configured routing system
- 📦 **Optimized Structure** - Well-organized project architecture
- ✅ **TypeScript** - Full TypeScript support with type safety
- 📱 **Responsive Design** - Mobile-first approach
- 🔧 **Developer Tools** - Enhanced DX with hot reload and debugging
- 🎯 **SEO Ready** - Built-in meta management and optimization
- 🚀 **Performance Optimized** - Code splitting and lazy loading

---

## 📁 Project Structure

```
my-nuxt-app/
├── app/
│   ├── components/     # Reusable Vue components
│   ├── layouts/        # Application layouts
│   ├── pages/          # Route pages
│   ├── plugins/        # Nuxt plugins
│   ├── middleware/     # Route middleware
│   └── stores/         # Pinia stores
├── public/             # Static assets
├── server/             # Server-side logic
├── types/              # TypeScript definitions
├── nuxt.config.ts      # Nuxt configuration
└── package.json        # Dependencies and scripts
```

---

## 🚀 Quick Start

### 1. Create New Project

```bash
# Using this template
npx nuxi init my-nuxt-app -t gh:AkbarshohIlhomovich/NUXT-TEMPLATE#main

# Navigate to project
cd my-nuxt-app
```

### 2. Install Dependencies

```bash
# Using npm
npm install

# Using yarn
yarn install

# Using pnpm (recommended)
pnpm install
```

### 3. Start Development Server

```bash
# Start dev server
npm run dev

# Or with other package managers
yarn dev
pnpm dev
```

Visit `http://localhost:3000` to see your application running! 🎉

---

## 📚 Available Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run generate     # Generate static site
npm run lint         # Run linting
npm run typecheck    # TypeScript type checking
```

---

## 🛠 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```bash
# API Configuration
NUXT_PUBLIC_API_BASE=https://api.example.com
NUXT_SECRET_KEY=your-secret-key

# Database
DATABASE_URL=your-database-url
```

### Nuxt Configuration

Key configurations in `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: [
    '@nuxt/ui',
    '@pinia/nuxt',
    '@nuxtjs/tailwindcss'
  ],
  css: ['~/assets/css/main.css'],
  runtimeConfig: {
    // Private keys (only available on server-side)
    secretKey: process.env.NUXT_SECRET_KEY,
    // Public keys (exposed to client-side)
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE
    }
  }
})
```

---

## 🎨 Using Nuxt UI Components

```vue
<template>
  <div>
    <UButton color="primary" size="lg">
      Click me!
    </UButton>
    
    <UCard class="mt-4">
      <template #header>
        <h3>Card Header</h3>
      </template>
      <p>Card content goes here</p>
    </UCard>
  </div>
</template>
```

---

## 🗂 State Management with Pinia

```typescript
// stores/counter.ts
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  
  const increment = () => {
    count.value++
  }
  
  const doubleCount = computed(() => count.value * 2)
  
  return { count, increment, doubleCount }
})
```

```vue
<!-- pages/index.vue -->
<template>
  <div>
    <p>Count: {{ counter.count }}</p>
    <p>Double: {{ counter.doubleCount }}</p>
    <UButton @click="counter.increment()">
      Increment
    </UButton>
  </div>
</template>

<script setup>
const counter = useCounterStore()
</script>
```

---

## 📱 Responsive Design

This template includes mobile-first responsive design:

- Tailwind CSS utilities for responsive breakpoints
- Nuxt UI components with built-in responsiveness
- Flexible layouts that adapt to screen sizes

---

## 🚢 Deployment

### Static Site Generation

```bash
npm run generate
```

Deploy the `dist/` folder to any static hosting service.

### Server-Side Rendering

```bash
npm run build
```

Deploy using platforms like:
- **Vercel** - `vercel deploy`
- **Netlify** - Connect your Git repository
- **DigitalOcean** - Use App Platform
- **Railway** - Connect and deploy

---

## 🤝 Contributing

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Nuxt Team** for the amazing framework
- **Tailwind CSS** for the utility-first CSS framework
- **Vue.js** community for continuous innovation
- **Pinia** team for excellent state management

---

## 📞 Support

If you have any questions or need help:

- 🐛 [Report Issues](https://github.com/AkbarshohIlhomovich/NUXT-TEMPLATE/issues)
- 💬 [Discussions](https://github.com/AkbarshohIlhomovich/NUXT-TEMPLATE/discussions)
- 📧 Contact: [your-email@example.com](mailto:your-email@example.com)

---

<div align="center">

**⭐ If this template helped you, please star the repository! ⭐**

Made with ❤️ by [@akbarwebdev](https://github.com/AkbarshohIlhomovich)

</div># 🚀 Nuxt 4 Professional Template

A modern, production-ready **Nuxt 4 Starter Template** featuring best practices, premium components, and developer experience optimizations.

Created by [@akbarwebdev](https://github.com/AkbarshohIlhomovich) 💻

---

## ✨ Features

- ⚡ **Nuxt 4** - Latest version with enhanced performance
- 🎨 **Nuxt UI** - Beautiful components with Tailwind CSS integration
- 🗂 **Pinia** - Intuitive state management solution
- 🔗 **Vue Router** - Pre-configured routing system
- 📦 **Optimized Structure** - Well-organized project architecture
- ✅ **TypeScript** - Full TypeScript support with type safety
- 📱 **Responsive Design** - Mobile-first approach
- 🔧 **Developer Tools** - Enhanced DX with hot reload and debugging
- 🎯 **SEO Ready** - Built-in meta management and optimization
- 🚀 **Performance Optimized** - Code splitting and lazy loading

---

## 📁 Project Structure

```
my-nuxt-app/
├── app/
│   ├── components/     # Reusable Vue components
│   ├── layouts/        # Application layouts
│   ├── pages/          # Route pages
│   ├── plugins/        # Nuxt plugins
│   ├── middleware/     # Route middleware
│   └── stores/         # Pinia stores
├── public/             # Static assets
├── server/             # Server-side logic
├── types/              # TypeScript definitions
├── nuxt.config.ts      # Nuxt configuration
└── package.json        # Dependencies and scripts
```

---

## 🚀 Quick Start

### 1. Create New Project

```bash
# Using this template
npx nuxi init my-nuxt-app -t gh:AkbarshohIlhomovich/NUXT-TEMPLATE#main

# Navigate to project
cd my-nuxt-app
```

### 2. Install Dependencies

```bash
# Using npm
npm install

# Using yarn
yarn install

# Using pnpm (recommended)
pnpm install
```

### 3. Start Development Server

```bash
# Start dev server
npm run dev

# Or with other package managers
yarn dev
pnpm dev
```

Visit `http://localhost:3000` to see your application running! 🎉

---

## 📚 Available Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run generate     # Generate static site
npm run lint         # Run linting
npm run typecheck    # TypeScript type checking
```

---

## 🛠 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```bash
# API Configuration
NUXT_PUBLIC_API_BASE=https://api.example.com
NUXT_SECRET_KEY=your-secret-key

# Database
DATABASE_URL=your-database-url
```

### Nuxt Configuration

Key configurations in `nuxt.config.ts`:

```typescript
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: [
    '@nuxt/ui',
    '@pinia/nuxt',
    '@nuxtjs/tailwindcss'
  ],
  css: ['~/assets/css/main.css'],
  runtimeConfig: {
    // Private keys (only available on server-side)
    secretKey: process.env.NUXT_SECRET_KEY,
    // Public keys (exposed to client-side)
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE
    }
  }
})
```

---

## 🎨 Using Nuxt UI Components

```vue
<template>
  <div>
    <UButton color="primary" size="lg">
      Click me!
    </UButton>
    
    <UCard class="mt-4">
      <template #header>
        <h3>Card Header</h3>
      </template>
      <p>Card content goes here</p>
    </UCard>
  </div>
</template>
```

---

## 🗂 State Management with Pinia

```typescript
// stores/counter.ts
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  
  const increment = () => {
    count.value++
  }
  
  const doubleCount = computed(() => count.value * 2)
  
  return { count, increment, doubleCount }
})
```

```vue
<!-- pages/index.vue -->
<template>
  <div>
    <p>Count: {{ counter.count }}</p>
    <p>Double: {{ counter.doubleCount }}</p>
    <UButton @click="counter.increment()">
      Increment
    </UButton>
  </div>
</template>

<script setup>
const counter = useCounterStore()
</script>
```

---

## 📱 Responsive Design

This template includes mobile-first responsive design:

- Tailwind CSS utilities for responsive breakpoints
- Nuxt UI components with built-in responsiveness
- Flexible layouts that adapt to screen sizes

---

## 🚢 Deployment

### Static Site Generation

```bash
npm run generate
```

Deploy the `dist/` folder to any static hosting service.

### Server-Side Rendering

```bash
npm run build
```

Deploy using platforms like:
- **Vercel** - `vercel deploy`
- **Netlify** - Connect your Git repository
- **DigitalOcean** - Use App Platform
- **Railway** - Connect and deploy

---

## 🤝 Contributing

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Nuxt Team** for the amazing framework
- **Tailwind CSS** for the utility-first CSS framework
- **Vue.js** community for continuous innovation
- **Pinia** team for excellent state management

---

## 📞 Support

If you have any questions or need help:

- 🐛 [Report Issues](https://github.com/AkbarshohIlhomovich/NUXT-TEMPLATE/issues)
- 💬 [Discussions](https://github.com/AkbarshohIlhomovich/NUXT-TEMPLATE/discussions)
- 📧 Contact: [your-email@example.com](mailto:your-email@example.com)

---

<div align="center">

**⭐ If this template helped you, please star the repository! ⭐**

Made with ❤️ by [@akbarwebdev](https://github.com/AkbarshohIlhomovich)

</div>