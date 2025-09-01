# Campus Super-App API Documentation

## Base URL
```
Production: https://api.campussuperapp.com
Staging: https://staging-api.campussuperapp.com
Development: http://localhost:4000/api
```

## Authentication

All protected endpoints require a Bearer token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

### Authentication Endpoints

#### POST /auth/register
Register a new user account.

**Request Body:**
```json
{
  "email": "student@university.edu",
  "username": "johnstudent",
  "password": "SecurePassword123!",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+1234567890",
  "role": "STUDENT"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Registration successful",
  "data": {
    "user": {
      "id": "cuid123",
      "email": "student@university.edu",
      "username": "johnstudent",
      "firstName": "John",
      "lastName": "Doe",
      "role": "STUDENT"
    },
    "tokens": {
      "accessToken": "jwt.token.here",
      "refreshToken": "refresh.token.here",
      "expiresIn": "7d"
    }
  }
}
```

#### POST /auth/login
Authenticate user and receive access tokens.

**Request Body:**
```json
{
  "email": "student@university.edu",
  "password": "SecurePassword123!"
}
```

#### POST /auth/refresh
Refresh access token using refresh token.

#### DELETE /auth/logout
Logout user and invalidate tokens.

---

## Delivery System API

### Orders

#### GET /delivery/orders
Get user's delivery orders with pagination and filtering.

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Items per page (default: 10)
- `status` (string): Filter by order status
- `shopId` (string): Filter by shop

**Response:**
```json
{
  "success": true,
  "data": {
    "orders": [
      {
        "id": "order123",
        "items": [
          {
            "name": "Burger",
            "quantity": 2,
            "price": 12.99
          }
        ],
        "totalAmount": 25.98,
        "status": "IN_TRANSIT",
        "estimatedTime": 25,
        "shop": {
          "name": "Campus Cafe",
          "location": "Building A"
        },
        "agent": {
          "name": "Delivery Guy",
          "phone": "+1234567890",
          "currentLocation": {
            "lat": 40.7128,
            "lng": -74.0060
          }
        }
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 5,
      "totalItems": 45
    }
  }
}
```

#### POST /delivery/orders
Create a new delivery order.

**Request Body:**
```json
{
  "shopId": "shop123",
  "items": [
    {
      "menuItemId": "item456",
      "quantity": 2,
      "customizations": ["No onions", "Extra cheese"]
    }
  ],
  "deliveryAddress": "Room 201, Hostel Block B",
  "contactNumber": "+1234567890",
  "specialInstructions": "Leave at door",
  "paymentMethod": "WALLET"
}
```

#### GET /delivery/orders/:id/track
Real-time tracking information for an order.

### Shops

#### GET /delivery/shops
Get list of available shops with their menus.

#### GET /delivery/shops/:id/menu
Get detailed menu for a specific shop.

---

## CodeQuest API

### Problems

#### GET /codequest/problems
Get coding problems with filtering and pagination.

**Query Parameters:**
- `difficulty` (string): EASY, MEDIUM, HARD
- `category` (string): Arrays, Strings, Dynamic Programming, etc.
- `tags` (string[]): Problem tags

**Response:**
```json
{
  "success": true,
  "data": {
    "problems": [
      {
        "id": "problem123",
        "title": "Two Sum",
        "difficulty": "EASY",
        "category": "Arrays",
        "tags": ["Array", "Hash Table"],
        "description": "Find two numbers that add up to target...",
        "constraints": "1 <= nums.length <= 10^4",
        "examples": [
          {
            "input": "[2,7,11,15], target = 9",
            "output": "[0,1]",
            "explanation": "nums[0] + nums[1] = 2 + 7 = 9"
          }
        ],
        "acceptanceRate": 0.47,
        "submissions": 2547893
      }
    ]
  }
}
```

#### POST /codequest/problems/:id/submit
Submit code solution for a problem.

**Request Body:**
```json
{
  "language": "javascript",
  "code": "function twoSum(nums, target) { /* solution */ }"
}
```

#### GET /codequest/submissions
Get user's submission history.

### AI Assistant

#### POST /codequest/ai/help
Get AI assistance for coding problems.

**Request Body:**
```json
{
  "problemId": "problem123",
  "question": "I'm getting a timeout error, can you help optimize my solution?",
  "currentCode": "function solution() { /* user code */ }"
}
```

#### POST /codequest/ai/voice
Process voice queries for coding help.

---

## Event Management API

### Events

#### GET /events
Get list of campus events.

**Query Parameters:**
- `category` (string): Workshop, Seminar, Sports, Cultural
- `startDate` (string): ISO date string
- `endDate` (string): ISO date string
- `status` (string): UPCOMING, ONGOING, COMPLETED

**Response:**
```json
{
  "success": true,
  "data": {
    "events": [
      {
        "id": "event123",
        "title": "AI Workshop Series",
        "description": "Learn about machine learning fundamentals",
        "category": "Workshop",
        "venue": "Computer Science Building, Room 101",
        "startTime": "2024-03-15T14:00:00Z",
        "endTime": "2024-03-15T16:00:00Z",
        "maxCapacity": 50,
        "registeredCount": 32,
        "isPaid": false,
        "organizer": {
          "name": "Dr. Smith",
          "department": "Computer Science"
        }
      }
    ]
  }
}
```

#### POST /events
Create a new campus event (Faculty/Admin only).

#### GET /events/:id/register
Register for an event.

#### POST /events/:id/checkin
QR-code based check-in for registered participants.

---

## E-Library API

### Notes

#### GET /library/notes
Search and browse study notes.

**Query Parameters:**
- `subject` (string): Subject/course name
- `tags` (string[]): Note tags
- `semester` (string): Academic semester
- `year` (string): Academic year
- `search` (string): Full-text search

**Response:**
```json
{
  "success": true,
  "data": {
    "notes": [
      {
        "id": "note123",
        "title": "Data Structures Lecture 5",
        "subject": "Computer Science",
        "description": "Binary trees and traversal algorithms",
        "tags": ["trees", "algorithms", "data-structures"],
        "semester": "Fall",
        "year": "2023",
        "professor": "Dr. Johnson",
        "fileType": "pdf",
        "fileSize": 2048576,
        "downloads": 245,
        "rating": 4.7,
        "uploadedBy": {
          "username": "student123",
          "year": 3
        },
        "createdAt": "2023-10-15T10:30:00Z"
      }
    ]
  }
}
```

#### POST /library/notes
Upload study notes or materials.

**Request Body (multipart/form-data):**
```
title: "Linear Algebra Notes"
subject: "Mathematics"
description: "Complete notes for linear algebra course"
tags: ["math", "linear-algebra", "vectors"]
semester: "Spring"
year: "2024"
professor: "Dr. Wilson"
file: [PDF file]
```

#### GET /library/notes/:id/download
Download a specific note file.

---

## Lost & Found API

### Items

#### GET /lostfound/items
Get lost and found items.

**Query Parameters:**
- `type` (string): LOST, FOUND
- `category` (string): Electronics, Books, Clothing, etc.
- `location` (string): Campus location
- `dateRange` (string): Recent, This Week, This Month

#### POST /lostfound/items
Report a lost or found item.

**Request Body:**
```json
{
  "type": "LOST",
  "title": "iPhone 14 Pro",
  "description": "Black iPhone with blue case, dropped near library",
  "category": "Electronics",
  "location": "Central Library",
  "dateLost": "2024-03-10T15:30:00Z",
  "contactInfo": "john.doe@university.edu",
  "reward": 50.00,
  "images": ["base64_encoded_image"]
}
```

#### POST /lostfound/items/:id/claim
Claim a found item with verification.

---

## Forum API

### Posts

#### GET /forum/posts
Get forum posts with filtering.

**Query Parameters:**
- `category` (string): Academic, Technical, General
- `tags` (string[]): Post tags
- `sort` (string): recent, popular, trending
- `answered` (boolean): Filter answered/unanswered

#### POST /forum/posts
Create a new forum post.

**Request Body:**
```json
{
  "title": "Need help with React hooks",
  "content": "I'm struggling with useEffect...",
  "category": "Technical",
  "tags": ["react", "javascript", "hooks"],
  "isAnonymous": false
}
```

#### POST /forum/posts/:id/answers
Answer a forum post.

#### POST /forum/posts/:id/vote
Vote on a post (upvote/downvote).

---

## Ride Sharing API

### Rides

#### GET /rides
Get available rides.

**Query Parameters:**
- `from` (string): Starting location
- `to` (string): Destination
- `date` (string): Travel date
- `seats` (number): Required seats

#### POST /rides
Offer a ride.

**Request Body:**
```json
{
  "fromLocation": "Campus Main Gate",
  "toLocation": "City Mall",
  "departureTime": "2024-03-15T18:00:00Z",
  "availableSeats": 3,
  "pricePerSeat": 15.00,
  "description": "Direct route, AC car",
  "vehicleInfo": {
    "make": "Honda",
    "model": "Civic",
    "color": "Blue",
    "plateNumber": "ABC123"
  }
}
```

#### POST /rides/:id/book
Book seats in a ride.

---

## Admin Dashboard API

### Analytics

#### GET /admin/analytics/overview
Get system-wide analytics overview.

**Response:**
```json
{
  "success": true,
  "data": {
    "users": {
      "total": 5247,
      "active": 4832,
      "newThisMonth": 234
    },
    "orders": {
      "totalToday": 89,
      "totalThisMonth": 2341,
      "revenue": 15678.90
    },
    "events": {
      "upcomingEvents": 12,
      "totalRegistrations": 1456
    },
    "systemHealth": {
      "apiResponseTime": 120,
      "databaseConnections": 45,
      "errorRate": 0.02
    }
  }
}
```

#### GET /admin/users
User management with filtering and search.

#### GET /admin/reports
Generate various system reports.

---

## WebSocket Events

The application uses Socket.IO for real-time features:

### Delivery Tracking
```javascript
// Join order tracking room
socket.emit('join-order-tracking', { orderId: 'order123' })

// Receive location updates
socket.on('order-location-update', (data) => {
  console.log('New location:', data.location)
})
```

### Live Notifications
```javascript
// Receive notifications
socket.on('notification', (notification) => {
  console.log('New notification:', notification)
})
```

### Forum Real-time Updates
```javascript
// Join post discussion
socket.emit('join-post', { postId: 'post123' })

// Receive new answers
socket.on('new-answer', (answer) => {
  console.log('New answer posted:', answer)
})
```

---

## Error Handling

All API endpoints follow consistent error response format:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": {
      "email": "Email is required",
      "password": "Password must be at least 8 characters"
    }
  },
  "timestamp": "2024-03-15T10:30:00Z"
}
```

### Common Error Codes
- `VALIDATION_ERROR` - Input validation failed
- `UNAUTHORIZED` - Invalid or missing authentication
- `FORBIDDEN` - Insufficient permissions
- `NOT_FOUND` - Resource not found
- `RATE_LIMIT_EXCEEDED` - Too many requests
- `INTERNAL_ERROR` - Server error

---

## Rate Limiting

API endpoints are rate-limited to prevent abuse:
- Authentication endpoints: 5 requests per minute
- General API: 100 requests per 15 minutes
- File uploads: 10 requests per hour
- Admin endpoints: 200 requests per 15 minutes

---

## Pagination

List endpoints support pagination:

**Request:**
```
GET /api/events?page=2&limit=20
```

**Response:**
```json
{
  "data": [...],
  "pagination": {
    "currentPage": 2,
    "totalPages": 15,
    "totalItems": 289,
    "hasNextPage": true,
    "hasPreviousPage": true
  }
}
```

---

For complete API documentation with interactive examples, visit the Swagger UI at `/api/docs` when the server is running.