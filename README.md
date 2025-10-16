# ASRT Commercial Spaces Website

A PHP-based commercial space rental platform with handyman services management.

## Project Structure

The project has been reorganized for better maintainability and clarity:

```
/
├── assets/                     # Static assets
│   └── css/                    # Stylesheets
│       └── style.css           # Main stylesheet
│
├── includes/                   # Reusable components
│   ├── header.php              # Site header with navigation
│   ├── footer.php              # Site footer
│   └── links.php               # Common links/includes
│
├── auth/                       # Authentication system
│   ├── login.php               # User login
│   ├── logout.php              # User logout
│   ├── register.php            # User registration
│   ├── verify_otp.php          # OTP verification
│   ├── send_otp_mail.php       # Send OTP email
│   ├── resend_otp.php          # Resend OTP
│   ├── send_forgot_otp.php     # Send password reset OTP
│   ├── verify_forgot_otp.php   # Verify password reset OTP
│   ├── resend_forgot_otp.php   # Resend password reset OTP
│   └── reset_password.php      # Password reset
│
├── pages/                      # Application pages
│   ├── dashboard.php           # User dashboard
│   ├── about.php               # About page
│   ├── handyman.php            # Handyman details
│   ├── handyman_type.php       # Handyman services listing
│   ├── maintenance.php         # Maintenance requests
│   ├── rent_request.php        # Rental request form
│   └── invoice_history.php     # Invoice history and payment
│
├── utils/                      # Utility classes
│   ├── class.phpmailer.php     # PHPMailer library
│   ├── class.smtp.php          # SMTP class
│   └── free_message_send.php   # Message sending utility
│
├── index.php                   # Main entry point (homepage)
├── test.php                    # Test file
└── try.php                     # Test file
```

## File Path Updates

After restructuring, all file paths have been updated to use absolute paths from the root:

### Navigation Links
- Home: `/index.php`
- About: `/pages/about.php`
- Dashboard: `/pages/dashboard.php`
- Services: `/pages/handyman_type.php`
- Maintenance: `/pages/maintenance.php`
- Payment: `/pages/invoice_history.php`

### Authentication
- Login: `/auth/login.php`
- Logout: `/auth/logout.php`
- Register: `/auth/register.php`

### Includes
- Header: `includes/header.php`
- Footer: `includes/footer.php`

### Utilities
- Send Message: `/utils/free_message_send.php`

## Database Configuration

The database configuration file should be located at:
```
../database/database.php
```

This path is relative to the subdirectories (auth, pages, utils).

## Key Features

1. **Commercial Space Rental**: Browse and rent available commercial units
2. **Handyman Services**: Request various handyman services (carpentry, electrical, plumbing, etc.)
3. **Invoice Management**: View and manage rental invoices
4. **Maintenance Requests**: Submit and track maintenance requests
5. **User Authentication**: Secure login/registration with OTP verification
6. **Admin Contact**: Direct communication channels with administrators

## Requirements

- PHP 7.4 or higher
- MySQL/MariaDB database
- Web server (Apache/Nginx)
- PHPMailer for email functionality

## Setup Instructions

1. Clone the repository
2. Configure the database connection in `../database/database.php`
3. Ensure proper file permissions for uploads directory
4. Configure email settings for OTP functionality
5. Access the website through your web server

## URL Structure

The website uses absolute paths from the root directory:
- Main page: `http://yoursite.com/index.php`
- Pages: `http://yoursite.com/pages/[page-name].php`
- Auth: `http://yoursite.com/auth/[auth-file].php`

## Benefits of New Structure

1. **Better Organization**: Files are grouped by functionality
2. **Easier Maintenance**: Clear separation of concerns
3. **Scalability**: Easy to add new features in appropriate directories
4. **Security**: Sensitive files are better organized
5. **Collaboration**: Team members can easily find and work on specific components

## Notes

- The `index.php` file remains in the root as the main entry point
- All internal links use absolute paths from the root
- Include files use relative paths from their location
- Database connections use relative paths (`../../database/database.php`)
