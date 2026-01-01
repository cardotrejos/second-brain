# Polar Credits Benefit Setup Guide

This document explains how to configure Polar's native **Credits Benefit** feature for automatic credit granting when customers purchase products.

## Overview

Instead of manually ingesting credit events via the API, we leverage Polar's built-in **Credits Benefit** attached to products. When a customer purchases a product with a Credits Benefit, Polar automatically adds credits to their meter balance.

## Prerequisites

- Access to Polar Dashboard (https://polar.sh)
- A configured Usage Meter (POLAR_METER_ID)
- Organization Access Token configured

## Step 1: Verify Your Meter Configuration

1. Navigate to **Meters** in the Polar dashboard sidebar
2. Ensure your usage meter is configured to:
   - Filter events with name `image_generation`
   - Use **Sum** aggregation on the `units` metadata field
3. Note the Meter ID - this is your `POLAR_METER_ID`

## Step 2: Configure Credit Packs with Credits Benefit

For each credit pack product, add a Credits Benefit:

### Starter Pack (10 Credits)

1. Navigate to **Products** → Select your Starter Pack product
2. Go to the **Benefits** section
3. Click **Add Benefit** → Select **Credits**
4. Configure:
   - **Meter**: Select your usage meter (POLAR_METER_ID)
   - **Amount**: `10`
   - **Description**: "10 image generation credits"
5. Save the product

### Popular Pack (50 Credits)

1. Navigate to **Products** → Select your Popular Pack product
2. Go to the **Benefits** section
3. Click **Add Benefit** → Select **Credits**
4. Configure:
   - **Meter**: Select your usage meter (POLAR_METER_ID)
   - **Amount**: `50`
   - **Description**: "50 image generation credits"
5. Save the product

### Pro Pack (200 Credits)

1. Navigate to **Products** → Select your Pro Pack product
2. Go to the **Benefits** section
3. Click **Add Benefit** → Select **Credits**
4. Configure:
   - **Meter**: Select your usage meter (POLAR_METER_ID)
   - **Amount**: `200`
   - **Description**: "200 image generation credits"
5. Save the product

## Step 3: Create Welcome Bonus Product (Free)

Create a $0 product that grants welcome credits to new users:

1. Navigate to **Products** → Click **Create Product**
2. Configure the product:
   - **Name**: "Welcome Bonus"
   - **Description**: "5 free credits for new users"
   - **Type**: One-Time Product
   - **Price**: $0.00 (free)
   - **Visibility**: Can be hidden from storefront (API-only checkout)
3. Add a **Credits Benefit**:
   - **Meter**: Select your usage meter (POLAR_METER_ID)
   - **Amount**: `5`
   - **Description**: "5 welcome credits"
4. Save the product
5. Copy the Product ID and add it to your environment as `POLAR_WELCOME_PRODUCT_ID`

## Step 4: Configure Webhook Events

Ensure your webhook endpoint is subscribed to these events:

1. Navigate to **Settings** → **Webhooks**
2. Select your webhook endpoint
3. Ensure these events are enabled:
   - `order.created` - For recording credit purchases
   - `customer.created` - For triggering welcome bonus
   - `customer.updated` - For tracking customer state changes

## Environment Variables

After completing the setup, update your `.env` file:

```bash
# Polar Configuration
POLAR_ACCESS_TOKEN=polar_oat_xxxxx
POLAR_WEBHOOK_SECRET=whsec_xxxxx
POLAR_METER_ID=meter_xxxxx

# Product IDs (with Credits Benefits attached)
POLAR_STARTER_PACK_ID=prod_xxxxx
POLAR_POPULAR_PACK_ID=prod_xxxxx
POLAR_PRO_PACK_ID=prod_xxxxx
POLAR_WELCOME_PRODUCT_ID=prod_xxxxx

# Public Product IDs (for client-side checkout)
NEXT_PUBLIC_POLAR_STARTER_PACK_ID=prod_xxxxx
NEXT_PUBLIC_POLAR_POPULAR_PACK_ID=prod_xxxxx
NEXT_PUBLIC_POLAR_PRO_PACK_ID=prod_xxxxx
```

## How It Works

### Purchase Flow

1. Customer initiates checkout for a credit pack
2. Polar processes the payment
3. Polar automatically grants the Credits Benefit to the customer's meter
4. `order.created` webhook fires → Our app records the transaction
5. Customer sees updated credit balance

### Welcome Flow

1. New user signs up → `customer.created` webhook fires
2. Our webhook handler creates a checkout for the free Welcome Bonus product
3. Polar processes the $0 order instantly
4. Polar automatically grants 5 credits via the Credits Benefit
5. `order.created` webhook fires → Our app records the welcome bonus transaction
6. User has 5 credits to start

## Key Benefits

- **Automatic**: Polar handles credit granting - no manual API calls needed
- **Reliable**: Leverages Polar's tested benefit system
- **Auditable**: All credits tied to orders visible in Polar dashboard
- **Consistent**: Same flow for all credit grants

## Troubleshooting

### Credits not appearing after purchase

1. Verify the Credits Benefit is attached to the product
2. Check the webhook logs in Polar dashboard
3. Ensure `order.created` webhook event is enabled
4. Check your application logs for webhook processing errors

### Welcome credits not granted

1. Verify `customer.created` webhook event is enabled
2. Check that `POLAR_WELCOME_PRODUCT_ID` is set correctly
3. Ensure the welcome product has a Credits Benefit attached
4. Check application logs for checkout creation errors

## Testing Guide

### Prerequisites

1. Configure sandbox environment in Polar dashboard
2. Set all `POLAR_*` environment variables for sandbox
3. Run the app locally with `bun run dev`

### Test Cases

#### 1. Welcome Credits (New User Signup)

1. Create a new user account via the signup form
2. Verify in Polar dashboard:
   - `customer.created` webhook was received
   - A checkout was created for the Welcome Bonus product
   - The order completed successfully
3. Verify in app:
   - User has 5 credits showing in dashboard
   - Credit history shows "Welcome credits" bonus entry

#### 2. Credit Pack Purchase

1. Log in as a test user
2. Navigate to pricing and purchase a credit pack
3. Complete the Polar checkout (use test card: 4242 4242 4242 4242)
4. Verify in Polar dashboard:
   - `order.created` webhook was received
   - Credits Benefit was applied to the customer
5. Verify in app:
   - Credits balance increased by the pack amount
   - Credit history shows the purchase

#### 3. Credit Usage

1. With credits available, generate an image
2. Verify in Polar dashboard:
   - `image_generation` event was ingested
   - Meter balance decreased
3. Verify in app:
   - Credits balance decreased by 1
   - Credit history shows usage entry

#### 4. Idempotency Check

1. Simulate a duplicate webhook by replaying an `order.created` event
2. Verify that credits are NOT double-granted
3. Check logs show "Duplicate order, skipping" message

### Common Issues

- **Credits not appearing**: Check webhook logs in Polar dashboard
- **Welcome bonus not granted**: Verify `POLAR_WELCOME_PRODUCT_ID` is set
- **Balance not updating**: Check that the meter ID matches in dashboard and env

## Related Documentation

- [Polar Credits Documentation](https://polar.sh/docs/features/usage-based-billing/credits)
- [Polar Meters Documentation](https://polar.sh/docs/features/usage-based-billing/meters)
- [Polar Webhooks Documentation](https://polar.sh/docs/integrate/webhooks/endpoints)
