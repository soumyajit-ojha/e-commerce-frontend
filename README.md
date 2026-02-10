# 🛰️ E-Commerce Frontend (Flipkart Mobile Clone)

E-Commerce Frontend is a high-performance React-based e-commerce storefront specialized for mobile devices. It mimics the **Flipkart UX**, featuring advanced filtering, role-based dashboards, and seamless integration with a FastAPI + S3 backend.

## 🚀 Tech Stack

- **Framework:** [React 18 (Vite)](https://vitejs.dev/)
- **Styling:** [Tailwind CSS v4](https://tailwindcss.com/) (CSS-first approach with `@theme`)
- **Icons:** [Lucide-React](https://lucide.dev/)
- **Routing:** [React Router DOM v6](https://reactrouter.com/)
- **HTTP Client:** [Axios](https://axios-http.com/)
- **State Management:** React Context API (Auth)

---

## ✨ Key Features

### 👤 User Management
- **RBAC (Role-Based Access Control):** Dedicated flows for **Buyers** and **Sellers**.
- **Auth Persistence:** Persistent sessions using `localStorage` and Header-based identification.
- **Account Layout:** Unified sidebar for Profile, Address Management, and Order History.
- **S3 Integration:** Real-time profile picture updates directly to AWS S3.

### 📱 Product Discovery
- **Dynamic Home Page:** Auto-generated budget categories (Premium, Mid-range, Budget) and horizontal scroll carousels.
- **Advanced Sidebar Filters:** Multi-select filtering by Brand, RAM, Storage, Network (5G/4G), and a dynamic Price Scroller.
- **Search Logic:** Real-time product discovery driven by backend query parameters.

### 🛒 Ecommerce Engine
- **State-Aware Cart:** "Add to Cart" button automatically transforms to "Go to Cart" if the item is already present.
- **Wishlist Toggle:** Iconic heart-icon toggle with instant UI feedback.
- **Price Snapshots:** Displays the price at the time of addition to ensure transparency.

### 🏭 Seller Central
- **Inventory Dashboard:** Real-time view of listed products with "Soft Delete" status.
- **Multipart Form Listing:** Support for binary image uploads (to S3) and technical specs for mobile phones.

---

## 📁 Project Structure

```text
src/
├── components/         # Reusable UI (Navbar, ProductCard, FilterSidebar, etc.)
├── context/            # Global State (AuthContext)
├── pages/              # Page Views (Home, Login, SellerDashboard, etc.)
├── services/           # API Abstraction Layer (api.js, userService.js, etc.)
├── styles/             # Modular CSS-first Tailwind styles
│   ├── main.css        # Entry point
│   ├── variables.css   # Custom theme variables (v4)
│   ├── auth.css        # Authentication layouts
│   └── navbar.css      # Header & Dropdown logic
└── App.jsx             # Router Configuration
```

---

## 🛠️ Getting Started

### 1. Installation
```bash
git clone <your-repo-url>
cd e-commerce-frontend
npm install
```

### 2. Environment Variables
Create a `.env` file in the root directory:
```env
VITE_API_URL=http://your-ec2-ip:8000
```

### 3. Development
```bash
npm run dev
```

---

## 🎨 Styling Architecture (Tailwind v4)

This project adopts the **Tailwind v4 "CSS-First"** approach. We do not use a `tailwind.config.js`. Instead:
- Variables are defined in `src/styles/variables.css` using the `@theme` block.
- Components use semantic class names (e.g., `.fk-input`, `.navbar-wrapper`) that utilize `@apply` for utility mapping.
- This ensures the JSX remains clean and the CSS remains maintainable.

---

## 🚢 Deployment (Vercel)

To avoid **Mixed Content Errors** (HTTPS calling HTTP EC2), the project uses a `vercel.json` rewrite:

```json
{
  "rewrites": [
    {
      "source": "/api/:path*",
      "destination": "http://your-ec2-ip:8000/:path*"
    }
  ]
}
```
In production, all API calls are made to the relative path `/api`, which Vercel proxies to your AWS backend securely.

---

## 🤝 Contributing
1. Ensure all new components follow the `.jsx` extension.
2. Use the `shopService` for any cart/wishlist logic to maintain snapshot integrity.
3. Use `FormData` for any service calls involving file uploads.