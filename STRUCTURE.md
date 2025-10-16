# Website Structure Documentation

## Before Restructuring

The original structure had all files in the root directory with no organization:

```
/
├── about.php
├── class.phpmailer.php
├── class.smtp.php
├── dashboard.php
├── footer.php
├── free_message_send.php
├── handyman.php
├── handyman_type.php
├── header.php
├── index.php
├── invoice_history.php
├── links.php
├── login.php
├── logout.php
├── maintenance.php
├── register.php
├── rent_request.php
├── resend_forgot_otp.php
├── resend_otp.php
├── reset_password.php
├── send_forgot_otp.php
├── send_otp_mail.php
├── style.css
├── test.php
├── try.php
├── verify_forgot_otp.php
└── verify_otp.php
```

**Problems with this structure:**
- ❌ Difficult to navigate
- ❌ Hard to maintain
- ❌ No clear separation of concerns
- ❌ Difficult for new developers to understand
- ❌ Hard to scale
- ❌ Security concerns with all files accessible

## After Restructuring

The new structure is organized by functionality:

```
/
├── assets/                          # Static Resources
│   └── css/
│       └── style.css                # Main stylesheet
│
├── includes/                        # Reusable Components
│   ├── header.php                   # Site header with navigation
│   ├── footer.php                   # Site footer
│   └── links.php                    # Common links/includes
│
├── auth/                            # Authentication System
│   ├── login.php                    # User login handler
│   ├── logout.php                   # User logout handler
│   ├── register.php                 # User registration
│   ├── verify_otp.php               # OTP verification for registration
│   ├── send_otp_mail.php            # Send OTP email
│   ├── resend_otp.php               # Resend registration OTP
│   ├── send_forgot_otp.php          # Send password reset OTP
│   ├── verify_forgot_otp.php        # Verify password reset OTP
│   ├── resend_forgot_otp.php        # Resend password reset OTP
│   └── reset_password.php           # Password reset handler
│
├── pages/                           # Application Pages
│   ├── dashboard.php                # User dashboard
│   ├── about.php                    # About page
│   ├── handyman.php                 # Handyman details
│   ├── handyman_type.php            # Handyman services listing
│   ├── maintenance.php              # Maintenance requests
│   ├── rent_request.php             # Rental request form
│   └── invoice_history.php          # Invoice history and payment
│
├── utils/                           # Utility Classes
│   ├── class.phpmailer.php          # PHPMailer library
│   ├── class.smtp.php               # SMTP class
│   └── free_message_send.php        # Message sending utility
│
├── index.php                        # Main entry point (homepage)
├── test.php                         # Test file
├── try.php                          # Test file
├── README.md                        # Project documentation
├── STRUCTURE.md                     # This file
├── .htaccess                        # Apache configuration
└── .gitignore                       # Git ignore rules
```

**Benefits of this structure:**
- ✅ Clear organization by functionality
- ✅ Easy to find specific files
- ✅ Better separation of concerns
- ✅ Easier to maintain and scale
- ✅ Professional structure
- ✅ Improved security with .htaccess rules
- ✅ Better for team collaboration

## File Path Changes

### Navigation Links (Updated to absolute paths)

| Old Path | New Path | Type |
|----------|----------|------|
| `index.php` | `/index.php` | Homepage |
| `about.php` | `/pages/about.php` | Page |
| `dashboard.php` | `/pages/dashboard.php` | Page |
| `handyman.php` | `/pages/handyman.php` | Page |
| `handyman_type.php` | `/pages/handyman_type.php` | Page |
| `maintenance.php` | `/pages/maintenance.php` | Page |
| `rent_request.php` | `/pages/rent_request.php` | Page |
| `invoice_history.php` | `/pages/invoice_history.php` | Page |
| `login.php` | `/auth/login.php` | Auth |
| `logout.php` | `/auth/logout.php` | Auth |
| `register.php` | `/auth/register.php` | Auth |
| `free_message_send.php` | `/utils/free_message_send.php` | Utility |

### Include Paths (Relative from subdirectories)

```php
// In pages/, auth/, utils/ directories:
require('../includes/header.php');
require('../includes/footer.php');

// In root directory (index.php):
require('includes/header.php');
require('includes/footer.php');
```

### Database Connection (Relative from subdirectories)

```php
// In pages/, auth/, utils/ directories:
require_once('../../database/database.php');

// In includes/ directory:
require_once(__DIR__ . '/../database/database.php');
```

## Migration Notes

1. All file movements were done using `git mv` to preserve history
2. All internal references and paths were updated
3. All redirects (Location headers) were updated
4. PHPMailer class references were updated
5. Form actions were updated to use absolute paths
6. Navigation links were updated to use absolute paths

## Security Improvements

The new `.htaccess` file includes:

1. **Security Headers:**
   - X-Frame-Options: Prevents clickjacking
   - X-XSS-Protection: Enables XSS filtering
   - X-Content-Type-Options: Prevents MIME sniffing
   - Referrer-Policy: Controls referrer information

2. **Access Control:**
   - Disabled directory browsing
   - Protected hidden files (starting with .)
   - Protected database configuration files

3. **Performance:**
   - Enabled compression for text files
   - Added browser caching rules
   - Optimized PHP settings

## Best Practices

1. **Use absolute paths** from root for all navigation links
2. **Use relative paths** for includes based on current file location
3. **Keep index.php in root** as the main entry point
4. **Organize new features** into appropriate directories
5. **Update documentation** when adding new directories or major files
6. **Follow naming conventions**:
   - Pages: descriptive names (e.g., `handyman_type.php`)
   - Auth: action-based names (e.g., `login.php`, `logout.php`)
   - Utils: class or function names (e.g., `class.phpmailer.php`)

## Future Enhancements

Consider these improvements for future development:

1. **Add config directory** for configuration files
2. **Add api directory** if building REST API endpoints
3. **Add models directory** for business logic classes
4. **Add controllers directory** for MVC pattern
5. **Add uploads directory** for user-uploaded files
6. **Add logs directory** for application logs
7. **Consider using Composer** for dependency management
8. **Implement autoloading** for classes
9. **Add tests directory** for unit tests
10. **Add documentation directory** for API docs
