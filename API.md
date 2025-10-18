# API Documentation

This document provides comprehensive API documentation for the PinkFlow ecosystem.

---

## Table of Contents

- [Overview](#overview)
- [Authentication](#authentication)
- [Base URL](#base-url)
- [API Endpoints](#api-endpoints)
  - [Authentication API](#authentication-api)
  - [Workspace API](#workspace-api)
  - [Governance API](#governance-api)
  - [User Profile API](#user-profile-api)
- [Real-time API (PinkSync)](#real-time-api-pinksync)
- [Error Handling](#error-handling)
- [Rate Limiting](#rate-limiting)
- [Changelog](#changelog)

---

## Overview

The PinkFlow API provides RESTful endpoints for managing authentication, workspaces, governance, and user profiles. Real-time features are provided through WebSocket connections via PinkSync.

### Key Features

- **RESTful Design**: Standard HTTP methods (GET, POST, PUT, DELETE)
- **JSON Format**: All requests and responses use JSON
- **JWT Authentication**: Secure token-based authentication
- **Real-time Updates**: WebSocket support for live collaboration
- **CORS Enabled**: Cross-origin resource sharing support

### API Status

**Current Status**: 🚧 In Development

The backend API is currently being implemented. This documentation describes the planned API structure. Endpoints marked with ✅ are implemented and available.

---

## Authentication

All API requests (except authentication endpoints) require a valid JWT token.

### Getting a Token

```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "user@example.com",
  "password": "secure_password"
}
```

**Response:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "user": {
    "id": "user123",
    "username": "user@example.com",
    "role": "developer"
  }
}
```

### Using the Token

Include the token in the Authorization header:

```http
GET /api/workspace/tree
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## Base URL

### Development
```
http://localhost:8000
```

### Production (when deployed)
```
https://api.mbtq.dev
```

---

## API Endpoints

### Authentication API

#### Login

**Status**: 🚧 Planned

```http
POST /api/auth/login
```

**Request Body:**
```json
{
  "username": "string",
  "password": "string"
}
```

**Response:** `200 OK`
```json
{
  "access_token": "string",
  "token_type": "bearer",
  "user": {
    "id": "string",
    "username": "string",
    "email": "string",
    "role": "developer|researcher|contributor",
    "fibonRoseProfile": {
      "trustScore": 0,
      "verifiedContributions": 0
    }
  }
}
```

**Errors:**
- `401 Unauthorized`: Invalid credentials
- `400 Bad Request`: Missing required fields

---

#### Logout

**Status**: 🚧 Planned

```http
POST /api/auth/logout
Authorization: Bearer {token}
```

**Response:** `200 OK`
```json
{
  "message": "Successfully logged out"
}
```

---

#### Get Current User

**Status**: 🚧 Planned

```http
GET /api/auth/user
Authorization: Bearer {token}
```

**Response:** `200 OK`
```json
{
  "id": "string",
  "username": "string",
  "email": "string",
  "role": "developer|researcher|contributor",
  "fibonRoseProfile": {
    "trustScore": 0,
    "verifiedContributions": 0,
    "badges": []
  }
}
```

---

### Workspace API

#### Get Workspace Tree

**Status**: 🚧 Planned

```http
GET /api/workspace/tree
Authorization: Bearer {token}
```

**Response:** `200 OK`
```json
{
  "files": [
    {
      "id": "string",
      "name": "string",
      "type": "file|directory",
      "path": "string",
      "children": []
    }
  ]
}
```

---

#### Get File Content

**Status**: 🚧 Planned

```http
GET /api/workspace/file?path={filePath}
Authorization: Bearer {token}
```

**Query Parameters:**
- `path` (required): File path relative to workspace root

**Response:** `200 OK`
```json
{
  "path": "string",
  "content": "string",
  "encoding": "utf-8",
  "lastModified": "ISO8601 timestamp"
}
```

**Errors:**
- `404 Not Found`: File doesn't exist
- `403 Forbidden`: No permission to access file

---

#### Update File Content

**Status**: 🚧 Planned

```http
PUT /api/workspace/file?path={filePath}
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "content": "string",
  "encoding": "utf-8"
}
```

**Response:** `200 OK`
```json
{
  "path": "string",
  "updated": true,
  "lastModified": "ISO8601 timestamp"
}
```

---

#### Create File

**Status**: 🚧 Planned

```http
POST /api/workspace/file
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "path": "string",
  "content": "string",
  "type": "file|directory"
}
```

**Response:** `201 Created`
```json
{
  "path": "string",
  "created": true,
  "timestamp": "ISO8601 timestamp"
}
```

**Errors:**
- `409 Conflict`: File already exists
- `400 Bad Request`: Invalid path or content

---

#### Commit Changes

**Status**: 🚧 Planned (Future)

```http
POST /api/workspace/commit
Authorization: Bearer {token}
Content-Type: application/json
```

**Request Body:**
```json
{
  "message": "string",
  "files": ["array of file paths"]
}
```

**Response:** `200 OK`
```json
{
  "commitId": "string",
  "message": "string",
  "timestamp": "ISO8601 timestamp"
}
```

---

### Governance API

#### List Ballots

**Status**: 🚧 Planned

```http
GET /api/governance/ballots
Authorization: Bearer {token}
```

**Query Parameters:**
- `status` (optional): `active|closed|all` (default: `active`)
- `page` (optional): Page number (default: 1)
- `limit` (optional): Results per page (default: 20, max: 100)

**Response:** `200 OK`
```json
{
  "ballots": [
    {
      "id": "string",
      "title": "string",
      "description": "string",
      "status": "active|closed",
      "vouchCount": 0,
      "threshold": 0,
      "createdAt": "ISO8601 timestamp",
      "expiresAt": "ISO8601 timestamp"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "pages": 5
  }
}
```

---

#### Vouch for Ballot

**Status**: 🚧 Planned

```http
POST /api/governance/ballots/{ballotId}/vouch
Authorization: Bearer {token}
```

**Request Body:** (optional)
```json
{
  "comment": "string"
}
```

**Response:** `200 OK`
```json
{
  "ballotId": "string",
  "vouched": true,
  "trustScore": 0,
  "vouchCount": 0
}
```

**Errors:**
- `403 Forbidden`: Insufficient trust score
- `409 Conflict`: Already vouched
- `404 Not Found`: Ballot doesn't exist

---

#### Get Approved Contributions

**Status**: 🚧 Planned

```http
GET /api/contributions/approved
Authorization: Bearer {token}
```

**Query Parameters:**
- `page` (optional): Page number
- `limit` (optional): Results per page

**Response:** `200 OK`
```json
{
  "contributions": [
    {
      "id": "string",
      "title": "string",
      "author": "string",
      "type": "code|documentation|design",
      "approvedAt": "ISO8601 timestamp",
      "vouchCount": 0
    }
  ]
}
```

---

### User Profile API

#### Sync FibonRose Profile

**Status**: 🚧 Planned

```http
POST /api/user/profile/sync
Authorization: Bearer {token}
```

**Response:** `200 OK`
```json
{
  "profile": {
    "userId": "string",
    "trustScore": 0,
    "verifiedContributions": 0,
    "badges": [],
    "lastSync": "ISO8601 timestamp"
  }
}
```

---

## Real-time API (PinkSync)

### WebSocket Connection

**Status**: 🚧 Planned

**Endpoint:** `ws://localhost:3001` (development)

### Connection

```javascript
const socket = io('ws://localhost:3001', {
  auth: {
    token: 'your-jwt-token'
  }
});
```

### Events

#### workspace:update

Emitted when workspace files change.

```javascript
socket.on('workspace:update', (data) => {
  // data: { path: string, action: 'create|update|delete' }
});
```

#### presence:update

Emitted when user presence changes.

```javascript
socket.on('presence:update', (data) => {
  // data: { users: Array<{ id, name, status }> }
});
```

#### notification

Emitted for user notifications.

```javascript
socket.on('notification', (data) => {
  // data: { type: string, message: string, timestamp: string }
});
```

---

## Error Handling

### Error Response Format

All errors follow this format:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  }
}
```

### Common HTTP Status Codes

- `200 OK`: Request successful
- `201 Created`: Resource created successfully
- `400 Bad Request`: Invalid request data
- `401 Unauthorized`: Missing or invalid authentication
- `403 Forbidden`: Insufficient permissions
- `404 Not Found`: Resource not found
- `409 Conflict`: Resource conflict
- `429 Too Many Requests`: Rate limit exceeded
- `500 Internal Server Error`: Server error

### Error Codes

- `AUTH_INVALID`: Invalid authentication credentials
- `AUTH_EXPIRED`: Token expired
- `AUTH_REQUIRED`: Authentication required
- `PERMISSION_DENIED`: Insufficient permissions
- `RESOURCE_NOT_FOUND`: Resource not found
- `VALIDATION_ERROR`: Request validation failed
- `RATE_LIMIT_EXCEEDED`: Too many requests
- `INTERNAL_ERROR`: Internal server error

---

## Rate Limiting

Rate limits are applied per user/IP address:

- **Authentication endpoints**: 5 requests per minute
- **Read operations**: 100 requests per minute
- **Write operations**: 30 requests per minute
- **WebSocket connections**: 10 per user

**Rate Limit Headers:**
```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1634567890
```

When rate limit is exceeded:

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 60

{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests. Please try again later.",
    "retryAfter": 60
  }
}
```

---

## Changelog

### Planned (v0.1.0)

- Initial API specification
- Authentication endpoints
- Workspace CRUD operations
- Governance voting system
- Real-time WebSocket support

### Future Enhancements

- GraphQL API (optional)
- Bulk operations
- Advanced search and filtering
- Webhooks for events
- API versioning strategy

---

## Support

For API support:

- **Issues**: [Report a bug](https://github.com/pinkycollie/PinkFlow/issues)
- **Documentation**: Check [README.md](README.md)
- **Security**: See [SECURITY.md](SECURITY.md)

---

**Last Updated**: 2025-10-17  
**API Version**: v0.1.0 (Planned)
