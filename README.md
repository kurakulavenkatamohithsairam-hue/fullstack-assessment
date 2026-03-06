# Stackline Full Stack Assessment

## Overview

This project is a sample eCommerce application that includes:

* Product List Page
* Search Results Page
* Product Detail Page

The purpose of this exercise was to review the application, identify issues, fix bugs, and document the improvements made.

---

## Issues Identified and Fixes

### 1. Product images not loading

**Issue**

Product images were not rendering correctly and the browser console showed an error related to the Next.js `Image` component.

**Fix**

Updated the `next.config.ts` configuration to allow images from the external domains used in the dataset.

```ts
images: {
  remotePatterns: [
    { protocol: "https", hostname: "m.media-amazon.com" },
    { protocol: "https", hostname: "images-na.ssl-images-amazon.com" }
  ]
}
```

**Reason**

Next.js restricts loading images from external domains unless they are explicitly configured. Adding these domains resolved the issue.

---

### 2. Runtime crash when product images were missing

**Issue**

During testing, the application crashed when a product did not contain image data. The UI attempted to access `imageUrls[0]`, which caused a runtime error when the array was undefined or empty.

**Fix**

Added a defensive check before rendering the image.

```tsx
product.imageUrls && product.imageUrls.length > 0
```

**Reason**

This prevents the application from attempting to access an image when none exists, improving application stability.

---

## Improvements and Validation

After fixing the issues above, the following flows were tested to verify the application works as expected:

* Loading the product list page
* Searching for products
* Filtering by category and subcategory
* Opening product detail pages
* Returning to the product list page
* Checking browser console logs for runtime errors

---

## Summary

The main issues discovered during testing were related to external image loading and a runtime crash caused by missing image data. Updating the Next.js configuration and adding defensive checks resolved these issues and improved the stability of the application.
