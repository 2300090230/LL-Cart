# 🧪 Quick Testing Guide - Frontend Migration

## ⚡ Quick Start

### 1. Start Backend
```bash
# Make sure Spring Boot backend is running on port 2004
# MongoDB should be connected
```

### 2. Start Frontend
```bash
cd D:\2NDYEAR\FSAD\SDP-PROJECT\REACTJS\frontend
npm start
```

### 3. Open Browser
```
http://localhost:3000
Press F12 to open DevTools → Console tab
```

---

## ✅ Testing Checklist (5 Minutes)

### Test 1: Home Page (1 min)
- [ ] Navigate to `http://localhost:3000`
- [ ] Verify product images load
- [ ] Check console - no 404 errors
- [ ] **Expected:** Images from Cloudinary or placeholder

### Test 2: Product Detail (1 min)
- [ ] Click on any product
- [ ] Verify product detail image loads
- [ ] Check related products images
- [ ] **Expected:** All images display correctly

### Test 3: Add to Cart (1 min)
- [ ] Login as buyer (if not logged in)
- [ ] Click "Add to Cart" on any product
- [ ] **Expected:** Success message, no errors in console
- [ ] Check Network tab - should see request to `/cart/add?buyerId=...`

### Test 4: View Cart (1 min)
- [ ] Navigate to cart page
- [ ] Verify cart item images load
- [ ] **Expected:** All cart items show correct images

### Test 5: View Orders (1 min)
- [ ] Navigate to orders page
- [ ] Verify order item images load
- [ ] **Expected:** All order items show correct images

---

## 🔍 What to Check in Console

### ✅ Good Signs
```
✓ No 404 errors
✓ No "ERR_NAME_NOT_RESOLVED"
✓ Images load from https://res.cloudinary.com/...
✓ Or fallback to https://placehold.co/...
✓ Add to Cart shows success message
```

### ❌ Red Flags
```
✗ GET .../displayproductimage 404
✗ Failed to add to cart
✗ Broken image icons
✗ TypeError: Cannot read property 'imageUrl'
```

---

## 🐛 Quick Fixes

### Issue: Images not loading
**Check:**
1. Backend running? `http://localhost:2004/product/viewallproducts`
2. Response has `imageUrl` field?
3. Clear browser cache: `Ctrl+Shift+Delete`

### Issue: Add to Cart fails
**Check:**
1. Logged in as buyer?
2. Check console error message
3. Network tab shows query parameters: `?buyerId=...&productId=...&quantity=...`

---

## 📊 Expected API Responses

### Get Products
```bash
curl http://localhost:2004/product/viewallproducts
```

**Should return:**
```json
[
  {
    "id": "...",
    "name": "Product Name",
    "imageUrl": "https://res.cloudinary.com/.../image.jpg",
    "cost": 99.99
  }
]
```

### Add to Cart
```bash
curl -X POST "http://localhost:2004/cart/add?buyerId=BUYER_ID&productId=PRODUCT_ID&quantity=1"
```

**Should return:**
```json
{
  "id": "cart_id",
  "quantity": 1,
  "product": {
    "id": "...",
    "name": "...",
    "imageUrl": "https://res.cloudinary.com/.../image.jpg"
  }
}
```

---

## 🎯 Success Criteria

All checks below should pass:

- ✅ Home page loads with product images
- ✅ Product detail page shows image
- ✅ Add to Cart works without errors
- ✅ Cart page shows cart item images
- ✅ Orders page shows order item images
- ✅ Seller products page shows images
- ✅ Update product shows preview image
- ✅ No 404 errors in console
- ✅ No `displayproductimage` requests

---

## 🚀 Full Test Scenarios

### Scenario 1: Buyer Flow
1. Go to home page
2. Browse products (images should load)
3. Click on a product
4. Add to cart (should succeed)
5. View cart (image should display)
6. Checkout (if implemented)
7. View orders (images should display)

### Scenario 2: Seller Flow
1. Login as seller
2. View products (images should load)
3. Update a product (preview should show existing image)
4. View orders (images should display)

### Scenario 3: Search & Navigation
1. Use search bar
2. Search results show images
3. Navigate through categories
4. All product images load correctly

---

## 📝 Notes

- **All images now come from:** Cloudinary CDN or fallback placeholder
- **Old endpoint removed:** `/product/displayproductimage`
- **Add to Cart format:** Query parameters (not JSON body)
- **Fallback images:** `https://placehold.co/...`

---

## ✅ When Everything Works

You should see:
- ✅ Product images loading fast (from CDN)
- ✅ Smooth image transitions
- ✅ No broken image icons
- ✅ Add to Cart working smoothly
- ✅ Clean console (no errors)

**🎉 Migration Successful!**

---

## 🆘 Need Help?

If you encounter issues:

1. **Check console** for error messages
2. **Check Network tab** for failed requests
3. **Test backend API** directly using curl
4. **Review MIGRATION_SUMMARY.md** for detailed documentation

---

**Last Updated:** November 16, 2025  
**Status:** All components migrated and tested
