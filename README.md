# Update WooCommerce Currency Symbol to the New SAR Symbol

Follow these steps to update the Saudi Riyal (SAR) currency symbol in your WooCommerce store to the new symbol (🇸🇦 ﷼) as per the Saudi Central Bank's 2025 update.

---

## Steps to Follow

### Step 1: Check for a Child Theme
- If your WooCommerce store already has a **child theme** activated, proceed to **Step 4**.
- If **no child theme** is available, follow the steps below.

---

### Step 2: Install the Child Theme Wizard Plugin
1. Click on the plugin name below to download it in a new browser tab:  
   [Child Theme Wizard](https://wordpress.org/plugins/child-theme-wizard/)
2. Install and activate the plugin.

---

### Step 3: Create a Child Theme
1. Use the **Child Theme Wizard** plugin to create a child theme based on your current active theme.
2. Once the child theme is created, **activate it** from the WordPress dashboard under **Appearance > Themes**.

---

### Step 4: Edit the `functions.php` File
1. Go to your WordPress dashboard.
2. Navigate to **Appearance > Theme File Editor**.
3. Select the **child theme** (if not already selected).
4. Locate and open the `functions.php` file.

---

### Step 5: Add the PHP Code
1. Copy the code below and paste it into the `functions.php` file of your child theme:

   ```php
   add_action('woocommerce_review_order_before_submit', 'add_custom_checkout_notice');
   //Saudi Arabia New Currency Symbols
   function change_saudi_riyal_currency_symbol($currency_symbol, $currency) {
    if ($currency === 'SAR') {
        
        global $pagenow;
        if (is_admin() && isset($_GET['page']) && $_GET['page'] === 'wc-admin') {
            return 'ر.س';        }

      
        $svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1124.14 1256.39" style="width: 0.7em; height: 0.7em; display: inline-block; vertical-align: middle; margin: 0 2px;">
            <path fill="currentColor" d="M699.62,1113.02h0c-20.06,44.48-33.32,92.75-38.4,143.37l424.51-90.24c20.06-44.47,33.31-92.75,38.4-143.37l-424.51,90.24Z"/>
            <path fill="currentColor" d="M1085.73,895.8c20.06-44.47,33.32-92.75,38.4-143.37l-330.68,70.33v-135.2l292.27-62.11c20.06-44.47,33.32-92.75,38.4-143.37l-330.68,70.27V66.13c-50.67,28.45-95.67,66.32-132.25,110.99v403.35l-132.25,28.11V0c-50.67,28.44-95.67,66.32-132.25,110.99v525.69l-295.91,62.88c-20.06,44.47-33.33,92.75-38.42,143.37l334.33-71.05v170.26l-358.3,76.14c-20.06,44.47-33.32,92.75-38.4,143.37l375.04-79.7c30.53-6.35,56.77-24.4,73.83-49.24l68.78-101.97v-.02c7.14-10.55,11.3-23.27,11.3-36.97v-149.98l132.25-28.11v270.4l424.53-90.28Z"/>
        </svg>';
        
     
        add_action('wp_head', function() {
            echo '<style>
                .custom-currency-symbol svg {
                    width: 0.7em;
                    height: 0.7em;
                    display: inline-block;
                    vertical-align: middle;
                    margin: 0 2px;
                }
            </style>';
        });
        
        return '<span class="custom-currency-symbol">' . $svg . '</span>';
    }
    return $currency_symbol;
   }
   add_filter('woocommerce_currency_symbol', 'change_saudi_riyal_currency_symbol', 10, 2);
