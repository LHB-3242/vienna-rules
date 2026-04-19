# Vienna RP - قوانين أمن الدولة - Contracts

## API Contracts

### Base URL
`/api`

### Models

#### Law (قانون)
```json
{
  "id": "string (UUID)",
  "title": "string",
  "content": "string",
  "category": "law",
  "created_at": "datetime",
  "updated_at": "datetime"
}
```

#### Protocol (بروتوكول)
```json
{
  "id": "string (UUID)",
  "title": "string",
  "content": "string",
  "category": "protocol",
  "created_at": "datetime",
  "updated_at": "datetime"
}
```

### API Endpoints

#### 1. Get All Laws
- **Endpoint:** `GET /api/laws`
- **Response:** Array of Law objects
- **Status:** 200 OK

#### 2. Get All Protocols
- **Endpoint:** `GET /api/protocols`
- **Response:** Array of Protocol objects
- **Status:** 200 OK

#### 3. Get Single Law/Protocol
- **Endpoint:** `GET /api/rules/:id`
- **Response:** Law or Protocol object
- **Status:** 200 OK | 404 Not Found

#### 4. Create Law/Protocol
- **Endpoint:** `POST /api/rules`
- **Request Body:**
```json
{
  "title": "string (required)",
  "content": "string (required)",
  "category": "law | protocol (required)"
}
```
- **Response:** Created object
- **Status:** 201 Created | 400 Bad Request

#### 5. Update Law/Protocol
- **Endpoint:** `PUT /api/rules/:id`
- **Request Body:**
```json
{
  "title": "string (optional)",
  "content": "string (optional)"
}
```
- **Response:** Updated object
- **Status:** 200 OK | 404 Not Found | 400 Bad Request

#### 6. Delete Law/Protocol
- **Endpoint:** `DELETE /api/rules/:id`
- **Response:** Success message
- **Status:** 200 OK | 404 Not Found

## Frontend-Backend Integration

### Mock Data to Replace

#### In StateSecurity.jsx
Replace:
```javascript
setLaws([...mock data...]);
```

With:
```javascript
const response = await axios.get(`${API}/laws`);
setLaws(response.data);
```

#### In StateProtocols.jsx
Replace:
```javascript
setProtocols([...mock data...]);
```

With:
```javascript
const response = await axios.get(`${API}/protocols`);
setProtocols(response.data);
```

#### In AdminPanel.jsx
Replace all mock operations with API calls:
- handleAdd → POST /api/rules
- handleUpdate → PUT /api/rules/:id
- handleDelete → DELETE /api/rules/:id
- Initial load → GET /api/laws or /api/protocols

## Database Schema

### Collection: rules

```javascript
{
  _id: ObjectId,
  id: String (UUID),
  title: String,
  content: String,
  category: String ("law" | "protocol"),
  created_at: DateTime,
  updated_at: DateTime
}
```

## Implementation Steps

1. ✅ Create frontend with mock data
2. ⏳ Create MongoDB models
3. ⏳ Implement API endpoints in FastAPI
4. ⏳ Replace mock data with API calls in frontend
5. ⏳ Test all CRUD operations
6. ⏳ Deploy and verify

## Notes

- All text fields support Arabic (RTL)
- UUID used for frontend compatibility
- MongoDB _id kept for database operations
- Created_at and updated_at automatically managed
- No authentication required for viewing laws/protocols
- Admin panel accessible at `/admin-vienna-rp` (URL-based security)
