---
hide:
  - navigation
---

# RentBnB - Multi-Tenant Property Rental Management System

A modern, scalable backend for a property rental management platform built with FastAPI, PostgreSQL, and Redis.

## Features

### Core Architecture
- **Multi-Tenant Architecture**: Complete tenant isolation with role-based access control and tenant-scoped data
- **Role-Based Access Control**: Support for SUPER_ADMIN, TENANT_ADMIN, MANAGER, and GUEST roles
- **Async Operations**: Full async/await support for high performance
- **Database Migrations**: Automated schema versioning with Alembic
- **Exception Handling**: Comprehensive error handling and validation with custom exception handlers
- **CORS Support**: Configured for frontend integration

### Authentication & Security
- **JWT Authentication**: Token-based authentication with access and refresh tokens
- **Passwordless OTP**: One-time password login sent via email
- **Email Verification**: Automated email-based account verification
- **Password Management**: Secure password hashing with bcrypt, forgot password/reset flow
- **Token Management**: Automatic token cleanup via scheduled tasks (every 6 hours)
- **Soft Delete Pattern**: Data retention with soft-delete for users, tenants, and other entities

### Property & Amenity Management
- **Property Management**: Complete CRUD operations for properties with multi-image support
- **Property Images**: Secure image uploads with UUID filenames and static file serving
- **Amenity System**: Manage property amenities with tenant-specific amenity catalogs
- **Property Categories**: Support for APARTMENT, HOUSE, VILLA, CONDO, etc.
- **Availability Tracking**: Real-time property availability checks

### Booking & Payment System
- **Booking System**: Full booking lifecycle management with status tracking (PENDING, CONFIRMED, CANCELLED, COMPLETED)
- **Availability Checks**: Prevent double-bookings with date range validation
- **Payment Integration**: Razorpay payment gateway with order creation and verification
- **Refund Processing**: Automated refund handling via Celery tasks
- **Payment Webhooks**: Real-time payment status updates via Razorpay webhooks
- **Payment Reconciliation**: Scheduled task to reconcile pending payments (every 2 minutes)

### Reviews & Ratings
- **Review System**: Guests can review properties after completed bookings
- **Rating Management**: 1-5 star ratings with review text
- **Review Validation**: Ensures only guests with completed bookings can review
- **Tenant Isolation**: Reviews are tenant-scoped

### Messaging & Real-time Communication
- **WebSocket Support**: Real-time bidirectional communication
- **Message System**: Persistent message storage with sender/receiver tracking
- **Message Types**: Support for TEXT, IMAGE, FILE message types
- **Real-time Notifications**: Instant message delivery via WebSockets

### Dashboard & Analytics
- **Tenant Dashboard**: Metrics for tenant admins (total properties, bookings, revenue, occupancy rate)
- **Platform Dashboard**: System-wide metrics for super admins (total tenants, users, properties, bookings, revenue)
- **Date Range Filtering**: Dashboard metrics support custom date ranges
- **Performance Optimized**: Database indexes for efficient metric aggregation

### Background Processing
- **Celery Worker**: Asynchronous task processing for emails, refunds, and bookings
- **Celery Beat**: Scheduled tasks for payment reconciliation and token cleanup
- **Email Tasks**: Async email sending for verification, password reset, and notifications
- **Booking Tasks**: Automated booking expiration handling
- **Payment Tasks**: Refund processing and payment reconciliation

### Caching & Storage
- **Redis Integration**: Caching for OTP, verification tokens, and session data
- **Static File Serving**: Dedicated endpoints for uploaded images and static assets
- **File Upload Handling**: Secure multipart file uploads with validation

## Tech Stack

- **Framework**: FastAPI 0.128+
- **Database**: PostgreSQL with async support (asyncpg)
- **Cache**: Redis 7.1+
- **Task Queue**: Celery 5.3+
- **Payment Gateway**: Razorpay
- **Authentication**: JWT with bcrypt password hashing
- **ORM**: SQLAlchemy 2.0+
- **Migrations**: Alembic 1.18+
- **Email**: aiosmtplib for async email
- **Python**: 3.13+

## Authentication & Security

### User Roles
- **SUPER_ADMIN**: Can manage all tenants and users system-wide
- **TENANT_ADMIN**: Manages their tenant and its users
- **MANAGER**: Works within their tenant (limited permissions)
- **GUEST**: View-only access within tenant

### Authentication Methods
- **Email & Password**: Traditional login with JWT tokens
- **Passwordless OTP**: One-time password sent to email
- **Token Refresh**: Long-lived refresh tokens for extended sessions
- **Email Verification**: Required for new accounts
- **Password Reset**: Secure password reset via email token

### Security Features
- Bcrypt password hashing
- JWT token-based authentication
- Soft-delete pattern for data retention
- Token blacklisting on logout
- Case-insensitive email/username lookups
- Role-based access control (RBAC)
- Multi-tenant isolation at database level