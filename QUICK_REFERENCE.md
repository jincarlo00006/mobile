# Quick Reference Guide

## Common File Paths

### Pages (User-facing)
- Homepage: `/index.php`
- Dashboard: `/pages/dashboard.php`
- About Us: `/pages/about.php`
- Services: `/pages/handyman_type.php`
- Maintenance: `/pages/maintenance.php`
- Payment: `/pages/invoice_history.php`
- Rent Request: `/pages/rent_request.php`

### Authentication
- Login: `/auth/login.php`
- Logout: `/auth/logout.php`
- Register: `/auth/register.php`
- Verify OTP: `/auth/verify_otp.php`
- Reset Password: `/auth/reset_password.php`

### Components
- Header: `includes/header.php`
- Footer: `includes/footer.php`
- Links: `includes/links.php`

### Utilities
- PHPMailer: `utils/class.phpmailer.php`
- SMTP: `utils/class.smtp.php`
- Send Message: `utils/free_message_send.php`

## How to Add New Features

### Adding a New Page

1. Create the PHP file in `/pages/` directory
2. Include header and footer:
```php
<?php
require('../includes/header.php');
?>

<!-- Your page content here -->

<?php
require('../includes/footer.php');
?>
```

3. Add navigation link in `includes/header.php`:
```php
<a class="modern-nav-link" href="/pages/your-new-page.php">
    <i class="bi bi-icon-name me-2"></i>Page Name
</a>
```

### Adding a New Auth Feature

1. Create the PHP file in `/auth/` directory
2. Use correct database path:
```php
require_once('../../database/database.php');
```

3. Redirect using absolute paths:
```php
header("Location: /index.php");
```

### Adding a New Utility

1. Create the PHP file in `/utils/` directory
2. Include in other files with:
```php
require_once(__DIR__ . '/../utils/your-utility.php');
```

### Adding New Styles

1. Add CSS to `assets/css/style.css`
2. Or create a new CSS file in `assets/css/` and link it in header

## Path Examples

### From Root Directory (index.php)
```php
require('includes/header.php');
require('includes/footer.php');
<a href="/pages/about.php">About</a>
<form action="/auth/login.php">
```

### From Pages Directory
```php
require('../includes/header.php');
require('../includes/footer.php');
require_once('../../database/database.php');
<a href="/index.php">Home</a>
<a href="/pages/dashboard.php">Dashboard</a>
<form action="/auth/logout.php">
```

### From Auth Directory
```php
require('../includes/header.php');  // If needed
require_once('../../database/database.php');
header("Location: /index.php");
header("Location: /pages/dashboard.php");
require_once(__DIR__ . '/../utils/class.phpmailer.php');
```

### From Utils Directory
```php
require_once('../../database/database.php');
header("Location: /index.php");
```

## Common Tasks

### Session Management
```php
// Start session (already in header.php)
if (session_status() === PHP_SESSION_NONE) {
    session_start();
}

// Check if logged in
$is_logged_in = isset($_SESSION['client_id']);

// Get user data
if ($is_logged_in) {
    $client_id = $_SESSION['client_id'];
    $username = $_SESSION['C_username'];
}
```

### Database Connection
```php
// Already included in header.php
$db = new Database();

// Use database methods
$users = $db->getClientByUsername($username);
```

### Redirects
```php
// Redirect to homepage
header("Location: /index.php");
exit();

// Redirect to dashboard
header("Location: /pages/dashboard.php");
exit();

// Redirect to login
header("Location: /auth/login.php");
exit();
```

### Forms
```php
<!-- Login Form -->
<form method="POST" action="/auth/login.php">
    <input type="text" name="username" required>
    <input type="password" name="password" required>
    <button type="submit">Login</button>
</form>

<!-- Page Navigation -->
<form method="get" action="/pages/handyman_type.php">
    <input type="hidden" name="jobtype_id" value="1">
    <button type="submit">View Service</button>
</form>
```

### Links
```php
<!-- Internal Links -->
<a href="/index.php">Home</a>
<a href="/pages/about.php">About</a>
<a href="/pages/dashboard.php">Dashboard</a>

<!-- External Links -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">External</a>

<!-- Email Links -->
<a href="mailto:management@asrt.space">Contact Us</a>

<!-- Phone Links -->
<a href="tel:+639451357685">Call Us</a>
```

## Troubleshooting

### Issue: Page not found (404)
**Solution:** Check that path uses absolute path from root (`/pages/file.php`)

### Issue: Include file not found
**Solution:** Check relative path from current file location:
- From pages: `../includes/header.php`
- From root: `includes/header.php`

### Issue: Database connection error
**Solution:** Verify database path:
- From pages/auth/utils: `../../database/database.php`
- From includes: `../database/database.php`

### Issue: Redirect not working
**Solution:** Ensure you're using absolute paths and have exit() after header():
```php
header("Location: /index.php");
exit();
```

### Issue: Styles not loading
**Solution:** Check that style.css is at `assets/css/style.css`

### Issue: PHPMailer class not found
**Solution:** From auth files, use:
```php
require_once(__DIR__ . '/../utils/class.phpmailer.php');
require_once(__DIR__ . '/../utils/class.smtp.php');
```

## File Naming Conventions

- **Pages:** Use descriptive names with underscores: `handyman_type.php`
- **Auth:** Use action names: `login.php`, `register.php`, `verify_otp.php`
- **Utils:** Use class or function names: `class.phpmailer.php`, `free_message_send.php`
- **Includes:** Use descriptive names: `header.php`, `footer.php`, `links.php`
- **CSS:** Use lowercase with hyphens: `style.css`, `custom-styles.css`

## Security Reminders

1. **Never expose database credentials** in public files
2. **Always validate and sanitize** user input
3. **Use prepared statements** for database queries
4. **Use password_hash()** for storing passwords
5. **Use password_verify()** for checking passwords
6. **Implement CSRF protection** for forms
7. **Use HTTPS** in production
8. **Keep .htaccess** security headers enabled
9. **Never trust client-side validation** alone
10. **Log security events** for monitoring

## Git Workflow

```bash
# Check status
git status

# Add changes
git add .

# Commit changes
git commit -m "Description of changes"

# Push to remote
git push origin branch-name

# Pull latest changes
git pull origin main
```

## Development Tips

1. **Test locally** before pushing to production
2. **Use error reporting** during development:
   ```php
   ini_set('display_errors', 1);
   error_reporting(E_ALL);
   ```
3. **Comment your code** for better maintainability
4. **Follow consistent indentation** (2 or 4 spaces)
5. **Use meaningful variable names**
6. **Keep functions small** and focused
7. **Avoid code duplication**
8. **Document complex logic**
9. **Use version control** effectively
10. **Test all user flows** after changes
