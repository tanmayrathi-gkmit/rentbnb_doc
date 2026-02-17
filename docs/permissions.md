---
hide:
  - navigation
---

# Role-Based Permission Matrix

This matrix defines what each role can do across all modules in the system. All permissions are tenant-scoped unless explicitly marked as "Global" (system-wide).

## Legend
- **Yes** - Full access to this operation
- **Own** - Can only access their own resources
- **Tenant** - Can access all resources within their tenant
- **No** - No access to this operation
- **Global** - System-wide access across all tenants

---

## Tenant Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Tenant | Yes (Global) | No | No | No |
| List All Tenants | Yes (Global) | No | No | No |
| View Tenant Details | Yes (Global) | Yes (Own) | Yes (Own) | Yes (Own) |
| Update Tenant | Yes (Global) | Yes (Own) | No | No |
| Delete Tenant | Yes (Global) | No | No | No |

---

## User Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Register User | Yes | Yes | Yes | Yes |
| List Users | Yes (Global) | Yes (Tenant) | No | No |
| View User Profile (Own) | Yes | Yes | Yes | Yes |
| View User Profile (Others) | Yes (Global) | Yes (Tenant) | No | No |
| Update User (Own) | Yes | Yes | Yes | Yes |
| Update User (Others) | Yes (Global) | Yes (Tenant) | No | No |
| Delete User (Own) | Yes | Yes | Yes | Yes |
| Delete User (Others) | Yes (Global) | Yes (Tenant) | No | No |
| Change User Role | Yes (Global) | Yes (Tenant) | No | No |

---

## Property Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Property | No | Yes (Tenant) | Yes (Tenant) | No |
| List Properties | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| View Property Details | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| Update Property | No | Yes (Tenant) | Yes (Tenant) | No |
| Delete Property | No | Yes (Tenant) | Yes (Tenant) | No |
| Upload Property Images | No | Yes (Tenant) | Yes (Tenant) | No |
| Delete Property Images | No | Yes (Tenant) | Yes (Tenant) | No |

> **Note**: SUPER_ADMIN does not have access to property management. This is tenant-scoped functionality managed by TENANT_ADMIN and MANAGER roles only.

---

## Amenity Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Amenity | Yes (Global) | No | No | No |
| List Amenities | Yes | Yes | Yes | Yes |
| View Amenity Details | Yes | Yes | Yes | Yes |
| Update Amenity | Yes (Global) | No | No | No |
| Delete Amenity | Yes (Global) | No | No | No |

> **Note**: Amenities are global system resources managed exclusively by SUPER_ADMIN. All users can view amenities, but only SUPER_ADMIN can create, update, or delete them.

---

## Booking Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Booking | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| List All Bookings | No | Yes (Tenant) | Yes (Tenant) | No |
| List Own Bookings | No | Yes | Yes | Yes |
| View Booking Details | No | Yes (Tenant) | Yes (Tenant) | Yes (Own) |
| Update Booking | No | Yes (Tenant) | Yes (Tenant) | Yes (Own) |
| Cancel Booking | No | Yes (Tenant) | Yes (Tenant) | Yes (Own) |
| Confirm Booking | No | Yes (Tenant) | Yes (Tenant) | No |

> **Note**: SUPER_ADMIN does not have access to booking management. This is tenant-scoped functionality.

---

## Payment Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Payment Order | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| Verify Payment | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| List All Payments | No | Yes (Tenant) | Yes (Tenant) | No |
| List Own Payments | No | Yes | Yes | Yes |
| View Payment Details | No | Yes (Tenant) | Yes (Tenant) | Yes (Own) |
| Process Refund | No | Yes (Tenant) | Yes (Tenant) | No |

> **Note**: SUPER_ADMIN does not have access to payment management. This is tenant-scoped functionality.

---

## Review Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Create Review | No | No | No | Yes* |
| List Reviews | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| View Review Details | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| Update Review | No | No | No | Yes (Own) |
| Delete Review | No | No | No | Yes (Own) |
| View Property Reviews | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |

**\*Note**: Reviews can only be created by GUEST users for properties with completed bookings. SUPER_ADMIN, TENANT_ADMIN, and MANAGER cannot create reviews.

---

## Message Management

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Send Message | No | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| List All Messages | No | Yes (Tenant) | No | No |
| List Own Messages | No | Yes | Yes | Yes |
| View Message Details | No | Yes (Tenant) | Yes (Own) | Yes (Own) |
| View Conversation | No | Yes (Tenant) | Yes (Own) | Yes (Own) |

> **Note**: SUPER_ADMIN does not have access to messaging. This is tenant-scoped functionality.

---

## Dashboard & Analytics

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| View Tenant Dashboard | Yes (Tenant) | Yes (Tenant) | No | No |
| View Platform Dashboard | Yes (Global) | No | No | No |
| Filter by Date Range | Yes | Yes | No | No |

**Tenant Dashboard Metrics**: Total properties, bookings, revenue, occupancy rate  
**Platform Dashboard Metrics**: Total tenants, users, properties, bookings, system-wide revenue

---

## WebSocket & Real-time Communication

| Operation | SUPER_ADMIN | TENANT_ADMIN | MANAGER | GUEST |
|-----------|-------------|--------------|---------|-------|
| Connect to WebSocket | Yes | Yes | Yes | Yes |
| Send Real-time Messages | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) | Yes (Tenant) |
| Receive Real-time Messages | Yes (Own) | Yes (Own) | Yes (Own) | Yes (Own) |

---

## Key Permission Principles

1. **Tenant Isolation**: All operational data (properties, bookings, payments, reviews, messages) is strictly tenant-scoped
2. **SUPER_ADMIN Limited Scope**: SUPER_ADMIN has global access ONLY to:
   - **Tenants**: Full CRUD operations across all tenants
   - **Users**: View, create, update, delete users across all tenants
   - **Amenities**: Global amenity catalog management
   - **Platform Dashboard**: System-wide analytics and metrics
3. **SUPER_ADMIN Restrictions**: SUPER_ADMIN does NOT have access to:
   - Properties, Bookings, Payments, Reviews, or Messages (all tenant-scoped)
   - These require tenant membership and appropriate role (TENANT_ADMIN, MANAGER, or GUEST)
4. **TENANT_ADMIN Privileges**: Full control within their tenant, including user management and all operational features
5. **MANAGER Privileges**: Can manage properties, amenities, bookings, and payments within their tenant
6. **GUEST Privileges**: Can create bookings, make payments, and write reviews for completed bookings
7. **Self-Service**: All roles can manage their own profile and view their own bookings/payments
8. **Review Restrictions**: Reviews can only be created by GUEST users for properties with completed bookings
9. **Message Privacy**: Users can only view conversations they are part of (except TENANT_ADMIN who can view all tenant messages)
