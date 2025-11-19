# DayFi Email Templates

This folder contains responsive HTML/CSS email templates for DayFi's user communication system. All templates are designed to be mobile-first and fully responsive across all device sizes.

## 📧 Available Templates

### Account & Authentication

#### 1. **Email Verification** (`email-verification.html`)
- **Subject:** Verify Your Email to Unlock Your DayFi Account ✉️
- **Purpose:** Send OTP for email verification during signup
- **Dynamic Data:** `{{firstName}}`, `{{lastName}}`, `{{otpCode}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 2. **Resend OTP** (`resend-otp.html`)
- **Subject:** Your New Verification Code 🔐
- **Purpose:** Generic OTP resend template for any verification scenario
- **Dynamic Data:** `{{firstName}}`, `{{otpCode}}`, `{{expiryMinutes}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 3. **Welcome Email** (`welcome-email.html`)
- **Subject:** Welcome to DayFi — Send Money Smarter 🌍
- **Purpose:** Onboard new users with feature highlights
- **Dynamic Data:** `{{firstName}}`, `{{lastName}}`

### Password Management

#### 4. **Password Reset Request** (`password-reset-request.html`)
- **Subject:** Reset Your DayFi Password 🔐
- **Purpose:** Send OTP verification code for password reset
- **Dynamic Data:** `{{firstName}}`, `{{otpCode}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 5. **Password Reset Success** (`password-reset-success.html`)
- **Subject:** Your Password Has Been Updated ✅
- **Purpose:** Confirm successful password reset with security warning
- **Dynamic Data:** `{{firstName}}`, `{{supportUrl}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

### Transaction PIN Management

#### 6. **Transaction PIN Verification** (`transaction-pin-verification.html`)
- **Subject:** Verify Your Identity to Reset Transaction PIN 🔐
- **Purpose:** Send OTP to verify user identity before allowing PIN reset
- **Dynamic Data:** `{{firstName}}`, `{{lastName}}`, `{{otpCode}}`, `{{expiryMinutes}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 7. **Transaction PIN Set Success** (`transaction-pin-set-success.html`)
- **Subject:** Your Transaction PIN Has Been Set ✅
- **Purpose:** Confirm successful transaction PIN setup with security warning
- **Dynamic Data:** `{{firstName}}`, `{{supportUrl}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

### Transfer Management

#### 8. **Transfer Successful** (`transfer-successful.html`)
- **Subject:** Your Transfer Was Successful 💸
- **Purpose:** Confirm successful transfer with next steps
- **Dynamic Data:** `{{firstName}}`, `{{amount}}`, `{{recipientName}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 9. **Transfer Unsuccessful** (`transfer-unsuccessful.html`)
- **Subject:** Transfer Unsuccessful — Let's Fix It ⚠️
- **Purpose:** Notify user of failed transfer with retry options
- **Dynamic Data:** `{{firstName}}`, `{{amount}}`, `{{recipientName}}`

#### 10. **Transfer Reminder** (`transfer-reminder.html`)
- **Subject:** Don't forget your transfer...
- **Purpose:** Remind users of incomplete transfers
- **Dynamic Data:** `{{firstName}}`, `{{lastName}}`, `{{amountToSend}}`, `{{amount}}`, `{{totalFee}}`

### Wallet Funding

#### 11. **Wallet Funded Successfully** (`fund-wallet-successful.html`)
- **Subject:** Your Wallet Has Been Funded 💰
- **Purpose:** Inform users that their wallet has been funded successfully
- **Dynamic Data:** `{{firstName}}`, `{{amount}}`, `{{balance}}`, `{{transactionId}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

#### 12. **Wallet Funding Failed** (`fund-wallet-failed.html`)
- **Subject:** Wallet Funding Failed ❌
- **Purpose:** Notify user of failed wallet funding with retry and support options
- **Dynamic Data:** `{{firstName}}`, `{{amount}}`, `{{failureReason}}`, `{{transactionId}}`, `{{supportUrl}}`, `{{faqUrl}}`, `{{googlePlayUrl}}`, `{{appStoreUrl}}`

## 🎨 Design Specifications

- **Font:** Karla (Google Fonts)
- **Background Color:** #FEF9F3 (light beige)
- **FAQ Button Color:** #6A31A2 (purple)
- **Text Color:** #000000 (black)
- **Layout:** Single-column, mobile-first responsive design

## 📱 Responsive Features

All templates include:
- **Mobile-first design** (320px+)
- **Tablet optimization** (768px+)
- **Desktop layout** (1024px+)
- **Flexible app store buttons** (stack vertically on mobile)
- **Readable typography** across all screen sizes

## 🔧 Backend Integration

### Template Variables
Replace the following placeholders with actual data:

```html
<!-- User Information -->
{{firstName}}          <!-- User's first name -->
{{lastName}}           <!-- User's last name -->

<!-- Transaction Data -->
{{amount}}             <!-- Transfer/funding amount -->
{{balance}}            <!-- User's wallet balance -->
{{amountToSend}}       <!-- Amount to be sent -->
{{totalFee}}           <!-- Transaction fee -->
{{recipientName}}      <!-- Recipient's name -->
{{transactionId}}      <!-- Unique transaction reference -->

<!-- Verification Codes -->
{{otpCode}}            <!-- OTP verification code -->
{{expiryMinutes}}      <!-- OTP expiry time in minutes -->

<!-- Error/Status Information -->
{{failureReason}}      <!-- Reason for transaction failure -->

<!-- URLs -->
{{faqUrl}}             <!-- FAQ page URL -->
{{supportUrl}}         <!-- Support contact URL -->
{{googlePlayUrl}}      <!-- Google Play Store URL -->
{{appStoreUrl}}        <!-- Apple App Store URL -->
```

### Implementation Example (Node.js/Express)

```javascript
const fs = require('fs');
const path = require('path');

// Load template
const template = fs.readFileSync(path.join(__dirname, 'password-reset-request.html'), 'utf8');

// Replace variables
const emailHtml = template
  .replace(/\{\{firstName\}\}/g, user.firstName)
  .replace(/\{\{otpCode\}\}/g, otpCode)
  .replace(/\{\{faqUrl\}\}/g, 'https://dayfi.com/faq')
  .replace(/\{\{googlePlayUrl\}\}/g, 'https://play.google.com/store/apps/details?id=com.dayfi.app')
  .replace(/\{\{appStoreUrl\}\}/g, 'https://apps.apple.com/app/dayfi/id123456789');

// Send email
await sendEmail({
  to: user.email,
  subject: 'Reset Your DayFi Password 🔐',
  html: emailHtml
});
```

### Implementation Example (Python/Django)

```python
from django.template.loader import render_to_string
from django.core.mail import send_mail

def send_password_reset_email(user, otp_code):
    context = {
        'firstName': user.first_name,
        'otpCode': otp_code,
        'faqUrl': 'https://dayfi.com/faq',
        'googlePlayUrl': 'https://play.google.com/store/apps/details?id=com.dayfi.app',
        'appStoreUrl': 'https://apps.apple.com/app/dayfi/id123456789'
    }
    
    html_content = render_to_string('emails/password-reset-request.html', context)
    
    send_mail(
        subject='Reset Your DayFi Password 🔐',
        message='',  # Plain text version
        html_message=html_content,
        from_email='noreply@dayfi.com',
        recipient_list=[user.email]
    )
```

## 📁 File Structure

```
dayfi_email_templates/
├── assets/
│   ├── apple.png              # Apple App Store button
│   └── google.png             # Google Play Store button
├── base-template.html         # Base template with common styles
├── email-verification.html    # Email verification OTP
├── resend-otp.html            # Generic OTP resend
├── welcome-email.html         # New user welcome
├── password-reset-request.html
├── password-reset-success.html
├── transaction-pin-verification.html
├── transaction-pin-set-success.html
├── transfer-successful.html
├── transfer-unsuccessful.html
├── transfer-reminder.html
├── fund-wallet-successful.html
├── fund-wallet-failed.html
├── preview.html               # Email preview/testing
└── README.md
```

## ✅ Testing Checklist

Before deploying, ensure:
- [ ] All templates render correctly in major email clients
- [ ] Dynamic data is properly replaced
- [ ] Images load correctly (app store buttons)
- [ ] Links are functional
- [ ] Mobile responsiveness works on various screen sizes
- [ ] Font loading works (Karla from Google Fonts)

## 🚀 Deployment Notes

1. **Email Client Compatibility:** Tested for Gmail, Outlook, Apple Mail, and Yahoo Mail
2. **Image Hosting:** Ensure app store button images are hosted on a reliable CDN
3. **Font Loading:** Karla font loads from Google Fonts (ensure internet connectivity)
4. **Fallback Fonts:** Arial and sans-serif are used as fallbacks

## 📞 Support

For questions about template implementation or customization, contact the development team.

---

**Created for DayFi** - Seamless, secure, and borderless money movement
