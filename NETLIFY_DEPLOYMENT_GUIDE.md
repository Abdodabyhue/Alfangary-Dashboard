# Netlify Deployment Guide

## Step 1: Connect to Netlify

1. Go to [netlify.com](https://netlify.com)
2. Click "Add new site" → "Import an existing project"
3. Connect your GitHub repository
4. Choose the branch (usually `main`)

## Step 2: Configure Build Settings

Netlify should auto-detect these settings, but verify:

```
Build command:     npm run build
Publish directory: dist
Functions folder:  netlify/functions
```

## Step 3: Set Environment Variables in Netlify

Go to: **Site Settings → Build & deploy → Environment**

Add these variables:

```
NODE_ENV = production
DATABASE_URL = postgresql://postgres.mjflqxgaclxqveakkjlr:%23%23Elfangary012@aws-1-eu-west-1.pooler.supabase.com:6543/postgres
CORS_ORIGIN = https://your-site-name.netlify.app
```

## Step 4: Deploy

1. Push your code to GitHub
2. Netlify automatically builds and deploys
3. Your app will be available at `https://your-site-name.netlify.app`

## Step 5: API Routes

Your API endpoints will be:

```
GET    https://your-site-name.netlify.app/api/orders
GET    https://your-site-name.netlify.app/api/menu
POST   https://your-site-name.netlify.app/api/orders
PUT    https://your-site-name.netlify.app/api/orders-update
POST   https://your-site-name.netlify.app/api/menu-add
PUT    https://your-site-name.netlify.app/api/menu-toggle
PUT    https://your-site-name.netlify.app/api/menu-update
```

These are routed through `netlify.toml` to your serverless functions.

## Troubleshooting

**CORS errors:**
- Update `CORS_ORIGIN` in environment variables to match your Netlify domain

**Database connection errors:**
- Verify `DATABASE_URL` is correct in Netlify environment variables
- Check Supabase IP whitelist allows Netlify servers

**Cold start delays:**
- First request may take 5-10 seconds (normal for serverless)
