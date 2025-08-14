# E-Commerce Admin Dashboard

## 📌 Overview
The E-Commerce Admin Dashboard is a full-stack admin interface built with **Next.js** and **Tailwind CSS** to manage an online store.  
It provides features for managing products, monitoring orders, and securely uploading product images to **AWS S3**.

---

## 🚀 Features
- **Authentication & Authorization** with [NextAuth.js](https://next-auth.js.org/) and MongoDB adapter.
- **Product Management**: Add, edit, delete, and list products.
- **Order Management**: View real-time orders, payment status, and customer details.
- **Image Uploads**: Securely upload product images to AWS S3.
- **Responsive UI** with TailwindCSS.
- **Drag-and-Drop Sorting** with React SortableJS.
- **Alerts & Feedback** using SweetAlert2.
- **Loading Indicators** with React Spinners.

---

## 🛠️ Tech Stack
### Frontend
- **Next.js 13**
- **React 18**
- **Tailwind CSS**
- **Axios** for API calls
- **React SortableJS**, **React SweetAlert2**, **React Spinners**

### Backend
- **Next.js API Routes**
- **MongoDB + Mongoose**
- **AWS S3** for file storage
- **Multiparty** for file uploads
- **NextAuth** for authentication
- **TypeORM** (legacy/optional dependency)

---

## 📂 Project Structure
pages/
├── index.js # Dashboard home
├── products.js # Product listing & CRUD links
├── orders.js # Orders table
├── api/
│ ├── products.js # Product CRUD APIs
│ ├── orders.js # Fetch orders from DB
│ ├── upload.js # Handle AWS S3 uploads
components/
├── Layout.js # Page wrapper with navigation
lib/
├── mongoose.js # MongoDB connection helper
models/
├── Product.js # Product schema
├── Order.js # Order schema


---

## ⚙️ How It Works

### **Authentication**
- The `_app.js` file wraps all pages in a `SessionProvider` so authentication state is available globally.
- Admin routes are protected using `isAdminRequest` in API endpoints.

### **Products**
1. `products.js` fetches product data from `/api/products` and renders it in a table.
2. Edit/Delete buttons link to dedicated product editing and deletion pages.
3. Adding a product involves uploading images via `/api/upload` before saving metadata in MongoDB.

### **Orders**
1. `orders.js` fetches order data from `/api/orders`.
2. Data includes date, payment status, recipient info, and purchased products.
3. Orders are sorted by creation date (latest first).

### **File Upload**
1. Frontend sends a multipart/form-data request to `/api/upload`.
2. Backend parses it with Multiparty, validates admin access, and uploads to AWS S3.
3. Returns public S3 URLs to be stored in MongoDB alongside product details.

---

## 🖥️ Installation & Setup
```bash
# Clone the repo
git clone https://github.com/your-username/ecommerce-admin.git
cd ecommerce-admin

# Install dependencies
npm install

# Create .env.local with:
# MONGODB_URI=your-mongodb-uri
# S3_ACCESS_KEY=your-aws-access-key
# S3_SECRET_ACCESS_KEY=your-aws-secret-key
# NEXTAUTH_SECRET=your-nextauth-secret
# NEXTAUTH_URL=http://localhost:3000

# Run the app
npm run dev
