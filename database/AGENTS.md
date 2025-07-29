# Database Technologies Guidelines for AI Agents (2025)

*Place this file in your database-related directories or project root for database guidance*

## Database Selection Framework (2025)

Based on the 2025 technology landscape, choose databases that align with your specific use case requirements:

### SQL Databases (Relational)
**Primary Choice: PostgreSQL 15+**
- **Use Cases**: Complex relationships, ACID compliance, financial data, reporting
- **Strengths**: Advanced features, JSON support, full-text search, mature ecosystem
- **Performance**: Excellent for complex queries, concurrent reads/writes
- **Scalability**: Vertical scaling, read replicas, partitioning

**Alternative: MySQL 8.0+**
- **Use Cases**: Web applications, content management, high-traffic websites
- **Strengths**: High performance, wide adoption, cloud support
- **Performance**: Optimized for read-heavy workloads
- **Scalability**: Read replicas, clustering solutions

### NoSQL Databases

#### Document Databases
**Primary Choice: MongoDB 7.0+**
- **Use Cases**: Content management, catalogs, user profiles, semi-structured data
- **Strengths**: Schema flexibility, horizontal scaling, developer productivity
- **Performance**: Excellent for read operations, aggregation pipelines
- **Scalability**: Built-in sharding, replica sets

#### Key-Value Stores
**Primary Choice: Redis 7.0+**
- **Use Cases**: Caching, session storage, real-time leaderboards, pub/sub
- **Strengths**: Extreme performance, data structures, clustering
- **Performance**: Sub-millisecond latency, high throughput
- **Scalability**: Redis Cluster, Redis Sentinel

#### Vector Databases (Emerging 2025)
**Primary Choices: Pinecone, Weaviate, or Milvus**
- **Use Cases**: AI applications, semantic search, recommendation engines
- **Strengths**: Similarity search, embeddings storage, AI integration
- **Performance**: Optimized for vector operations and similarity queries
- **Scalability**: Distributed vector indexing and search

## PostgreSQL Best Practices

### Schema Design Principles
```sql
-- Use UUIDs for distributed systems
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- User table with proper constraints and indexes
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    email VARCHAR(255) UNIQUE NOT NULL,
    email_verified BOOLEAN DEFAULT FALSE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    role VARCHAR(50) DEFAULT 'user' CHECK (role IN ('admin', 'user', 'moderator')),
    avatar_url TEXT,
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE
);

-- Indexes for performance
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
CREATE INDEX idx_users_created_at ON users(created_at);
CREATE INDEX idx_users_deleted_at ON users(deleted_at) WHERE deleted_at IS NULL;
CREATE INDEX idx_users_metadata ON users USING GIN(metadata);

-- Full-text search index
CREATE INDEX idx_users_search ON users USING GIN(
    to_tsvector('english', first_name || ' ' || last_name || ' ' || email)
);
```

### Advanced PostgreSQL Features
```sql
-- JSONB for flexible schema
CREATE TABLE user_preferences (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    preferences JSONB NOT NULL DEFAULT '{}',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- JSONB indexes for performance
CREATE INDEX idx_preferences_user_id ON user_preferences(user_id);
CREATE INDEX idx_preferences_data ON user_preferences USING GIN(preferences);

-- Partial indexes for specific queries
CREATE INDEX idx_preferences_theme ON user_preferences((preferences->>'theme')) 
WHERE preferences ? 'theme';

-- Function-based index for computed values
CREATE INDEX idx_users_full_name ON users(LOWER(first_name || ' ' || last_name));

-- Composite indexes for common query patterns
CREATE INDEX idx_users_role_created ON users(role, created_at) WHERE deleted_at IS NULL;

-- Conditional unique constraints
CREATE UNIQUE INDEX idx_users_email_active ON users(email) WHERE deleted_at IS NULL;
```

### Database Triggers and Functions
```sql
-- Automatic updated_at trigger
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $
BEGIN
    NEW.updated_at = NOW();
    RETURN NEW;
END;
$ language 'plpgsql';

-- Apply trigger to tables
CREATE TRIGGER update_users_updated_at 
    BEFORE UPDATE ON users 
    FOR EACH ROW 
    EXECUTE FUNCTION update_updated_at_column();

-- Audit log function
CREATE OR REPLACE FUNCTION create_audit_log()
RETURNS TRIGGER AS $
BEGIN
    INSERT INTO audit_logs (
        table_name,
        operation,
        old_data,
        new_data,
        user_id,
        timestamp
    ) VALUES (
        TG_TABLE_NAME,
        TG_OP,
        CASE WHEN TG_OP = 'DELETE' THEN row_to_json(OLD) ELSE NULL END,
        CASE WHEN TG_OP IN ('INSERT', 'UPDATE') THEN row_to_json(NEW) ELSE NULL END,
        COALESCE(NEW.updated_by, OLD.updated_by),
        NOW()
    );
    RETURN COALESCE(NEW, OLD);
END;
$ language 'plpgsql';
```

### Query Optimization Patterns
```sql
-- Use EXPLAIN ANALYZE for query optimization
EXPLAIN (ANALYZE, BUFFERS, VERBOSE) 
SELECT u.*, p.preferences 
FROM users u 
LEFT JOIN user_preferences p ON u.id = p.user_id 
WHERE u.role = 'user' 
    AND u.created_at > NOW() - INTERVAL '30 days'
    AND u.deleted_at IS NULL
ORDER BY u.created_at DESC 
LIMIT 20;

-- Efficient pagination with cursor-based approach
SELECT * FROM users 
WHERE created_at < $1  -- cursor timestamp
    AND deleted_at IS NULL
ORDER BY created_at DESC 
LIMIT 20;

-- Efficient search with full-text search
SELECT *, ts_rank(search_vector, plainto_tsquery('english', $1)) as rank
FROM users 
WHERE search_vector @@ plainto_tsquery('english', $1)
    AND deleted_at IS NULL
ORDER BY rank DESC, created_at DESC
LIMIT 20;

-- Use CTEs for complex queries
WITH recent_users AS (
    SELECT id, email, created_at
    FROM users 
    WHERE created_at > NOW() - INTERVAL '7 days'
        AND deleted_at IS NULL
),
user_stats AS (
    SELECT 
        COUNT(*) as total_users,
        COUNT(CASE WHEN email_verified THEN 1 END) as verified_users
    FROM recent_users
)
SELECT * FROM user_stats;
```

## MongoDB Best Practices

### Collection Design Patterns
```javascript
// User document schema with embedded and referenced data
{
  "_id": ObjectId("..."),
  "email": "user@example.com",
  "emailVerified": false,
  "passwordHash": "...",
  "profile": {
    "firstName": "John",
    "lastName": "Doe",
    "avatar": "https://...",
    "preferences": {
      "theme": "dark",
      "language": "en",
      "notifications": {
        "email": true,
        "push": false
      }
    }
  },
  "roles": ["user"],
  "metadata": {
    "loginCount": 15,
    "lastLoginAt": ISODate("2025-01-01T00:00:00.000Z"),
    "ipAddresses": ["192.168.1.1", "10.0.0.1"]
  },
  "createdAt": ISODate("2025-01-01T00:00:00.000Z"),
  "updatedAt": ISODate("2025-01-01T00:00:00.000Z"),
  "deletedAt": null
}

// Indexes for performance
db.users.createIndex({ "email": 1 }, { unique: true, sparse: true })
db.users.createIndex({ "roles": 1 })
db.users.createIndex({ "createdAt": 1 })
db.users.createIndex({ "deletedAt": 1 }, { sparse: true })
db.users.createIndex({ 
  "profile.firstName": "text", 
  "profile.lastName": "text", 
  "email": "text" 
})

// Compound indexes for common queries
db.users.createIndex({ 
  "roles": 1, 
  "createdAt": -1, 
  "deletedAt": 1 
})

// Partial indexes for specific conditions
db.users.createIndex(
  { "email": 1 },
  { 
    partialFilterExpression: { "emailVerified": true },
    name: "idx_verified_emails"
  }
)
```

### Aggregation Pipeline Patterns
```javascript
// Complex aggregation for user analytics
db.users.aggregate([
  // Match active users from last 30 days
  {
    $match: {
      createdAt: { $gte: new Date(Date.now() - 30 * 24 * 60 * 60 * 1000) },
      deletedAt: { $exists: false }
    }
  },
  
  // Add computed fields
  {
    $addFields: {
      fullName: { $concat: ["$profile.firstName", " ", "$profile.lastName"] },
      daysSinceCreated: {
        $divide: [
          { $subtract: [new Date(), "$createdAt"] },
          1000 * 60 * 60 * 24
        ]
      }
    }
  },
  
  // Group by role and calculate metrics
  {
    $group: {
      _id: "$roles",
      count: { $sum: 1 },
      avgDaysSinceCreated: { $avg: "$daysSinceCreated" },
      verifiedCount: {
        $sum: { $cond: ["$emailVerified", 1, 0] }
      }
    }
  },
  
  // Sort by count descending
  { $sort: { count: -1 } }
])

// Lookup pattern for joining collections
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "user",
      pipeline: [
        { $project: { email: 1, "profile.firstName": 1, "profile.lastName": 1 } }
      ]
    }
  },
  { $unwind: "$user" },
  {
    $project: {
      total: 1,
      createdAt: 1,
      "user.email": 1,
      "user.profile": 1
    }
  }
])
```

### Schema Validation
```javascript
// JSON Schema validation for collections
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["email", "passwordHash", "profile", "createdAt"],
      properties: {
        email: {
          bsonType: "string",
          pattern: "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$",
          description: "Must be a valid email address"
        },
        emailVerified: {
          bsonType: "bool",
          description: "Email verification status"
        },
        passwordHash: {
          bsonType: "string",
          minLength: 60,
          description: "Hashed password"
        },
        profile: {
          bsonType: "object",
          required: ["firstName", "lastName"],
          properties: {
            firstName: {
              bsonType: "string",
              minLength: 1,
              maxLength: 100
            },
            lastName: {
              bsonType: "string",
              minLength: 1,
              maxLength: 100
            },
            avatar: {
              bsonType: "string"
            },
            preferences: {
              bsonType: "object"
            }
          }
        },
        roles: {
          bsonType: "array",
          items: {
            bsonType: "string",
            enum: ["admin", "user", "moderator"]
          }
        },
        createdAt: {
          bsonType: "date"
        },
        updatedAt: {
          bsonType: "date"
        },
        deletedAt: {
          bsonType: ["date", "null"]
        }
      }
    }
  },
  validationAction: "error",
  validationLevel: "strict"
})
```

## Redis Best Practices

### Caching Patterns
```javascript
// User session caching
const sessionKey = `session:${userId}:${sessionId}`;
await redis.setex(sessionKey, 3600, JSON.stringify(sessionData)); // 1 hour TTL

// API response caching with cache invalidation
const cacheKey = `api:users:${page}:${limit}:${filters}`;
const cached = await redis.get(cacheKey);

if (cached) {
  return JSON.parse(cached);
}

const result = await fetchUsersFromDatabase(page, limit, filters);
await redis.setex(cacheKey, 300, JSON.stringify(result)); // 5 minutes TTL

// Cache invalidation on data change
await redis.del(`api:users:*`); // Simple approach
// Or use Redis patterns for more sophisticated invalidation
await redis.eval(`
  for i, key in ipairs(redis.call('keys', ARGV[1])) do
    redis.call('del', key)
  end
`, 0, 'api:users:*');
```

### Rate Limiting
```javascript
// Sliding window rate limiting
async function checkRateLimit(userId, action, limit, windowSizeSeconds) {
  const key = `rate_limit:${userId}:${action}`;
  const now = Date.now();
  const windowStart = now - (windowSizeSeconds * 1000);
  
  // Remove expired entries and count current requests
  const pipeline = redis.pipeline();
  pipeline.zremrangebyscore(key, 0, windowStart);
  pipeline.zcard(key);
  pipeline.zadd(key, now, now);
  pipeline.expire(key, windowSizeSeconds);
  
  const results = await pipeline.exec();
  const currentCount = results[1][1];
  
  return {
    allowed: currentCount < limit,
    remaining: Math.max(0, limit - currentCount - 1),
    resetTime: windowStart + (windowSizeSeconds * 1000)
  };
}

// Usage
const { allowed, remaining } = await checkRateLimit(
  userId, 
  'api_call', 
  100, // 100 requests
  3600 // per hour
);
```

### Pub/Sub for Real-time Features
```javascript
// Real-time notification system
class NotificationService {
  constructor(redisClient) {
    this.redis = redisClient;
    this.subscriber = redisClient.duplicate();
  }

  async publishNotification(userId, notification) {
    const channel = `notifications:${userId}`;
    await this.redis.publish(channel, JSON.stringify({
      id: generateId(),
      type: notification.type,
      title: notification.title,
      message: notification.message,
      data: notification.data,
      timestamp: Date.now()
    }));
  }

  async subscribeToUserNotifications(userId, callback) {
    const channel = `notifications:${userId}`;
    await this.subscriber.subscribe(channel);
    
    this.subscriber.on('message', (receivedChannel, message) => {
      if (receivedChannel === channel) {
        const notification = JSON.parse(message);
        callback(notification);
      }
    });
  }

  async publishToChannel(channel, message) {
    await this.redis.publish(channel, JSON.stringify(message));
  }
}

// Real-time metrics updates
await redis.publish('metrics:update', JSON.stringify({
  type: 'user_count',
  value: await getUserCount(),
  timestamp: Date.now()
}));
```

## Vector Database Implementation (2025)

### Pinecone Configuration
```python
# Python example for Pinecone vector database
import pinecone
from sentence_transformers import SentenceTransformer

# Initialize Pinecone
pinecone.init(
    api_key="your-api-key",
    environment="your-env"
)

# Create index for semantic search
index_name = "document-search"
if index_name not in pinecone.list_indexes():
    pinecone.create_index(
        name=index_name,
        dimension=384,  # Sentence transformer dimension
        metric="cosine"
    )

index = pinecone.Index(index_name)

# Initialize embedding model
model = SentenceTransformer('all-MiniLM-L6-v2')

# Store document embeddings
def store_document(doc_id, text, metadata=None):
    embedding = model.encode(text).tolist()
    index.upsert(vectors=[{
        "id": doc_id,
        "values": embedding,
        "metadata": metadata or {}
    }])

# Semantic search
def search_documents(query, top_k=10, filter_metadata=None):
    query_embedding = model.encode(query).tolist()
    
    results = index.query(
        vector=query_embedding,
        top_k=top_k,
        include_metadata=True,
        filter=filter_metadata
    )
    
    return results['matches']

# Usage examples
store_document(
    doc_id="doc_1",
    text="Machine learning algorithms for natural language processing",
    metadata={"category": "AI", "author": "John Doe"}
)

# Search with metadata filtering
results = search_documents(
    query="artificial intelligence techniques",
    top_k=5,
    filter_metadata={"category": "AI"}
)
```

### Weaviate Configuration
```javascript
// JavaScript example for Weaviate
import weaviate from 'weaviate-ts-client';

const client = weaviate.client({
  scheme: 'http',
  host: 'localhost:8080',
});

// Define schema
const schema = {
  class: 'Document',
  vectorizer: 'text2vec-openai',
  moduleConfig: {
    'text2vec-openai': {
      model: 'ada',
      modelVersion: '002',
      type: 'text'
    }
  },
  properties: [
    {
      name: 'title',
      dataType: ['string'],
    },
    {
      name: 'content',
      dataType: ['text'],
    },
    {
      name: 'category',
      dataType: ['string'],
    },
    {
      name: 'author',
      dataType: ['string'],
    },
    {
      name: 'publishedAt',
      dataType: ['date'],
    }
  ]
};

// Create schema
await client.schema
  .classCreator()
  .withClass(schema)
  .do();

// Store documents
async function storeDocument(document) {
  return await client.data
    .creator()
    .withClassName('Document')
    .withProperties(document)
    .do();
}

// Semantic search with hybrid approach
async function searchDocuments(query, options = {}) {
  const {
    limit = 10,
    where = null,
    certainty = 0.7
  } = options;

  let queryBuilder = client.graphql
    .get()
    .withClassName('Document')
    .withFields('title content category author publishedAt _additional { certainty }')
    .withNearText({ concepts: [query] })
    .withLimit(limit);

  if (where) {
    queryBuilder = queryBuilder.withWhere(where);
  }

  const result = await queryBuilder.do();
  
  return result.data.Get.Document.filter(
    doc => doc._additional.certainty >= certainty
  );
}

// Usage
await storeDocument({
  title: "Introduction to Vector Databases",
  content: "Vector databases are specialized systems for storing and querying high-dimensional vectors...",
  category: "Database",
  author: "Jane Smith",
  publishedAt: "2025-01-01T00:00:00.000Z"
});

const results = await searchDocuments(
  "vector database applications",
  {
    limit: 5,
    where: {
      path: ['category'],
      operator: 'Equal',
      valueText: 'Database'
    }
  }
);
```

## Database Migration Strategies

### PostgreSQL Migrations
```sql
-- Migration: 001_create_users_table.sql
BEGIN;

CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_created_at ON users(created_at);

COMMIT;

-- Migration: 002_add_user_roles.sql
BEGIN;

-- Add role column
ALTER TABLE users ADD COLUMN role VARCHAR(50) DEFAULT 'user';
ALTER TABLE users ADD CONSTRAINT check_user_role 
    CHECK (role IN ('admin', 'user', 'moderator'));

-- Add index for role queries
CREATE INDEX idx_users_role ON users(role);

-- Update existing users to have default role
UPDATE users SET role = 'user' WHERE role IS NULL;

-- Make role NOT NULL
ALTER TABLE users ALTER COLUMN role SET NOT NULL;

COMMIT;

-- Migration: 003_add_soft_deletes.sql
BEGIN;

-- Add deleted_at column for soft deletes
ALTER TABLE users ADD COLUMN deleted_at TIMESTAMP WITH TIME ZONE;

-- Create partial index for active users
CREATE INDEX idx_users_active ON users(id) WHERE deleted_at IS NULL;

-- Update unique constraint to only apply to active users
DROP INDEX users_email_key;
CREATE UNIQUE INDEX idx_users_email_unique ON users(email) WHERE deleted_at IS NULL;

COMMIT;
```

### MongoDB Schema Evolution
```javascript
// Migration: Add email verification fields
db.users.updateMany(
  { emailVerified: { $exists: false } },
  { 
    $set: { 
      emailVerified: false,
      emailVerificationToken: null,
      emailVerificationExpires: null
    }
  }
);

// Migration: Restructure profile data
db.users.updateMany(
  { firstName: { $exists: true } },
  [
    {
      $set: {
        profile: {
          firstName: "$firstName",
          lastName: "$lastName",
          avatar: "$avatar",
          preferences: {
            theme: { $ifNull: ["$theme", "light"] },
            language: { $ifNull: ["$language", "en"] }
          }
        }
      }
    },
    {
      $unset: ["firstName", "lastName", "avatar", "theme", "language"]
    }
  ]
);

// Migration: Add indexes after schema change
db.users.createIndex({ "profile.firstName": "text", "profile.lastName": "text" });
db.users.createIndex({ "profile.preferences.theme": 1 });
```

## Performance Monitoring and Optimization

### PostgreSQL Performance Monitoring
```sql
-- Monitor slow queries
SELECT 
    query,
    calls,
    total_time,
    mean_time,
    rows,
    100.0 * shared_blks_hit / nullif(shared_blks_hit + shared_blks_read, 0) AS hit_percent
FROM pg_stat_statements 
ORDER BY total_time DESC 
LIMIT 10;

-- Check index usage
SELECT 
    schemaname,
    tablename,
    indexname,
    idx_tup_read,
    idx_tup_fetch,
    idx_scan
FROM pg_stat_user_indexes 
ORDER BY idx_scan ASC;

-- Monitor table statistics
SELECT 
    schemaname,
    tablename,
    seq_scan,
    seq_tup_read,
    idx_scan,
    idx_tup_fetch,
    n_tup_ins,
    n_tup_upd,
    n_tup_del
FROM pg_stat_user_tables 
ORDER BY seq_scan DESC;

-- Check for missing indexes
SELECT 
    schemaname,
    tablename,
    seq_scan,
    seq_tup_read,
    seq_tup_read / seq_scan AS avg_seq_tup_read
FROM pg_stat_user_tables 
WHERE seq_scan > 0 
ORDER BY seq_tup_read DESC 
LIMIT 10;
```

### MongoDB Performance Monitoring
```javascript
// Enable profiling for slow operations
db.setProfilingLevel(2, { slowms: 100 });

// View slow operations
db.system.profile.find()
  .sort({ ts: -1 })
  .limit(5)
  .pretty();

// Index usage statistics
db.users.aggregate([
  { $indexStats: {} }
]);

// Collection statistics
db.users.stats();

// Explain query execution
db.users.find({ "profile.firstName": "John" }).explain("executionStats");

// Monitor replica set status
rs.status();

// Check sharding status (if using sharding)
sh.status();
```

## Security Best Practices

### Database Security Checklist
```yaml
# PostgreSQL Security Configuration
# postgresql.conf
ssl = on
ssl_cert_file = 'server.crt'
ssl_key_file = 'server.key'
ssl_ca_file = 'ca.crt'
ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL'
password_encryption = scram-sha-256
log_connections = on
log_disconnections = on
log_statement = 'ddl'

# pg_hba.conf
# TYPE  DATABASE        USER            ADDRESS                 METHOD
local   all             postgres                               peer
host    all             all             127.0.0.1/32           scram-sha-256
host    all             all             ::1/128                scram-sha-256
hostssl all             all             0.0.0.0/0              scram-sha-256
```

### Application-Level Security
```typescript
// Database connection with security
import { Pool } from 'pg';

const pool = new Pool({
  host: process.env.DB_HOST,
  port: parseInt(process.env.DB_PORT || '5432'),
  database: process.env.DB_NAME,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  ssl: {
    rejectUnauthorized: true,
    ca: fs.readFileSync('ca.crt'),
    cert: fs.readFileSync('client.crt'),
    key: fs.readFileSync('client.key'),
  },
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});

// Always use parameterized queries
async function getUserByEmail(email: string) {
  const query = 'SELECT * FROM users WHERE email = $1 AND deleted_at IS NULL';
  const result = await pool.query(query, [email]);
  return result.rows[0];
}

// Input validation and sanitization
function validateAndSanitizeUserInput(input: any) {
  // Use Zod or similar for validation
  const schema = z.object({
    email: z.string().email(),
    firstName: z.string().min(1).max(100),
    lastName: z.string().min(1).max(100),
  });
  
  return schema.parse(input);
}
```

## Backup and Recovery Strategies

### PostgreSQL Backup
```bash
#!/bin/bash
# Automated backup script

DB_NAME="your_database"
BACKUP_DIR="/backups/postgresql"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="$BACKUP_DIR/${DB_NAME}_${DATE}.sql"

# Create backup directory if it doesn't exist
mkdir -p $BACKUP_DIR

# Create database dump
pg_dump -h localhost -U postgres $DB_NAME > $BACKUP_FILE

# Compress the backup
gzip $BACKUP_FILE

# Remove backups older than 7 days
find $BACKUP_DIR -name "*.gz" -mtime +7 -delete

# Upload to cloud storage (example with AWS S3)
aws s3 cp "${BACKUP_FILE}.gz" s3://your-backup-bucket/postgresql/
```

### MongoDB Backup
```bash
#!/bin/bash
# MongoDB backup script

DB_NAME="your_database"
BACKUP_DIR="/backups/mongodb"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_PATH="$BACKUP_DIR/$DATE"

# Create backup
mongodump --host localhost:27017 --db $DB_NAME --out $BACKUP_PATH

# Compress backup
tar -czf "${BACKUP_PATH}.tar.gz" -C $BACKUP_DIR $DATE

# Clean up uncompressed backup
rm -rf $BACKUP_PATH

# Remove old backups
find $BACKUP_DIR -name "*.tar.gz" -mtime +7 -delete

# Upload to cloud storage
aws s3 cp "${BACKUP_PATH}.tar.gz" s3://your-backup-bucket/mongodb/
```

## Database Selection Decision Matrix

### Use Case Decision Framework

| Use Case | Recommended Database | Why |
|----------|---------------------|-----|
| E-commerce Platform | PostgreSQL + Redis | ACID compliance for transactions, Redis for cart/session |
| Content Management | MongoDB | Flexible schema for varied content types |
| Real-time Analytics | ClickHouse or TimescaleDB | Optimized for time-series and analytical queries |
| Social Media | PostgreSQL + Redis + Graph DB | Relational data + caching + social graph |
| IoT Data | InfluxDB or TimescaleDB | Time-series optimization for sensor data |
| Search Engine | Elasticsearch + PostgreSQL | Full-text search + metadata storage |
| AI/ML Applications | Vector DB + PostgreSQL | Embeddings + structured data |
| Gaming Leaderboards | Redis + PostgreSQL | Real-time scores + persistent data |
| Financial Systems | PostgreSQL | ACID compliance, regulatory requirements |
| Document Storage | MongoDB + GridFS | Document-oriented with file storage |

### Performance Considerations
- **Read-Heavy**: PostgreSQL with read replicas, MongoDB with replica sets
- **Write-Heavy**: MongoDB with sharding, Redis for very high throughput
- **Complex Queries**: PostgreSQL for complex JOINs and analytics
- **Simple Queries**: MongoDB for document-based simple queries
- **Real-time**: Redis for sub-millisecond operations
- **Large Scale**: Distributed databases (Cassandra, MongoDB sharding)