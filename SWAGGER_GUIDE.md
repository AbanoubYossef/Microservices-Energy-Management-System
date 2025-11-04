# Swagger/OpenAPI Documentation Guide

This guide explains how to access and use the Swagger UI documentation for the Energy Management System microservices.

## Overview

All three microservices now have interactive Swagger UI documentation powered by `drf-spectacular`. This provides:
- Interactive API documentation
- Try-it-out functionality to test endpoints
- Request/response schemas
- Authentication support

## Accessing Swagger UI

Once the services are running, you can access the Swagger UI at:

### Auth Service
- **Swagger UI**: http://localhost:8000/api/docs/
- **OpenAPI Schema**: http://localhost:8000/api/schema/

### User Service
- **Swagger UI**: http://localhost:8001/api/docs/
- **OpenAPI Schema**: http://localhost:8001/api/schema/

### Device Service
- **Swagger UI**: http://localhost:8002/api/docs/
- **OpenAPI Schema**: http://localhost:8002/api/schema/

## Using Swagger UI

### 1. Testing Public Endpoints (No Authentication)

For endpoints like `/api/auth/register/` and `/api/auth/login/`:
1. Click on the endpoint to expand it
2. Click "Try it out"
3. Fill in the request body
4. Click "Execute"
5. View the response

### 2. Testing Protected Endpoints (With Authentication)

For endpoints that require authentication:

1. **Get a JWT Token**:
   - Go to Auth Service Swagger UI
   - Use `/api/auth/login/` endpoint
   - Copy the `access` token from the response

2. **Authorize in Swagger**:
   - Click the "Authorize" button (lock icon) at the top right
   - Enter: `Bearer <your-access-token>`
   - Click "Authorize"
   - Click "Close"

3. **Test Protected Endpoints**:
   - Now all requests will include the JWT token
   - Try any protected endpoint

### 3. Example: Complete Flow

```bash
# 1. Register a new user
POST /api/auth/register/
{
  "username": "testuser",
  "password": "testpass123",
  "role": "user"
}

# 2. Login to get token
POST /api/auth/login/
{
  "username": "testuser",
  "password": "testpass123"
}

# Response includes:
{
  "tokens": {
    "access": "eyJ0eXAiOiJKV1QiLCJhbGc...",
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGc..."
  }
}

# 3. Use the access token to authorize in Swagger UI
# Click "Authorize" and enter: Bearer eyJ0eXAiOiJKV1QiLCJhbGc...

# 4. Now test protected endpoints like:
GET /api/auth/users/
GET /api/devices/
```

## Installation & Setup

The Swagger dependencies are already added to `requirements.txt` for all services:

```bash
# Install dependencies for each service
cd auth_service && pip install -r requirements.txt
cd ../user_service && pip install -r requirements.txt
cd ../device_service && pip install -r requirements.txt
```

Or using Docker:
```bash
docker-compose up --build
```

## API Endpoints Summary

### Auth Service (Port 8000)
- `POST /api/auth/register/` - Register new user
- `POST /api/auth/login/` - Login and get JWT token
- `GET /api/auth/validate/` - Validate JWT token
- `GET /api/auth/users/` - List all users (Admin only)
- `GET /api/auth/users/{id}/` - Get user info
- `PUT /api/auth/users/{id}/update/` - Update user
- `DELETE /api/auth/users/{id}/delete/` - Delete user (Admin only)

### User Service (Port 8001)
- `POST /api/users/create/` - Create user (internal)
- `GET /api/users/` - List all users
- `GET /api/users/{id}/` - Get user details
- `PUT /api/users/{id}/update/` - Update user
- `DELETE /api/users/{id}/delete/` - Delete user
- `POST /api/users/{id}/rollback/` - Rollback user creation

### Device Service (Port 8002)
- `POST /api/users/create/` - Create user mapping (internal)
- `PUT /api/users/{id}/update/` - Update user mapping
- `DELETE /api/users/{id}/` - Delete user mapping
- `POST /api/users/{id}/rollback/` - Rollback user mapping
- `GET /api/devices/` - List all devices
- `POST /api/devices/create/` - Create device
- `GET /api/devices/{id}/` - Get device details
- `PUT /api/devices/{id}/update/` - Update device
- `DELETE /api/devices/{id}/delete/` - Delete device
- `POST /api/devices/assign/` - Assign device to user
- `POST /api/devices/{id}/unassign/` - Unassign device
- `GET /api/users/{id}/devices/` - Get user's devices
- `GET /api/mappings/` - List all user-device mappings

## Customization

The Swagger settings can be customized in each service's `settings.py`:

```python
SPECTACULAR_SETTINGS = {
    'TITLE': 'Your API Title',
    'DESCRIPTION': 'Your API Description',
    'VERSION': '1.0.0',
    'SERVE_INCLUDE_SCHEMA': False,
    'COMPONENT_SPLIT_REQUEST': True,
}
```

## Troubleshooting

### Swagger UI not loading
- Ensure the service is running
- Check that `drf-spectacular` is installed
- Verify the service is accessible at the correct port

### Authentication not working
- Make sure you're using the format: `Bearer <token>`
- Check that the token hasn't expired (default: 5 hours)
- Verify you're using the `access` token, not the `refresh` token

### Endpoints not showing up
- Run migrations: `python manage.py migrate`
- Restart the service
- Clear browser cache

## Additional Resources

- [drf-spectacular Documentation](https://drf-spectacular.readthedocs.io/)
- [OpenAPI Specification](https://swagger.io/specification/)
- [Django REST Framework](https://www.django-rest-framework.org/)
