# VideoHub Deployment Guide

## Render.com Deployment

### Prerequisites
1. Create a Render account at https://render.com
2. Create a new PostgreSQL 16 database on Render
3. Get the database connection string

### Step 1: Database Setup
1. Go to Render Dashboard → Databases
2. Create new PostgreSQL database:
   - Name: `videohub-db`
   - Database Name: `videohub`
   - User: `videohub`
   - Region: Choose closest to your users
   - Plan: Free tier available

### Step 2: Deploy Application
1. Connect your GitHub repository to Render
2. Create a new Web Service:
   - Environment: `Node`
   - Build Command: `npm install && npm run build`
   - Start Command: `npm start`
   - Auto-Deploy: `Yes`

### Step 3: Environment Variables
Set these environment variables in Render:
- `NODE_ENV`: `production`
- `DATABASE_URL`: Your PostgreSQL connection string from Step 1

### Step 4: Database Migration
After deployment, run the database migration:
```bash
npm run db:push
```

### Step 5: File Storage
The application stores uploaded videos and thumbnails in the `/uploads` directory.
For production, consider:
- Using Render's persistent disk for file storage
- Migrating to cloud storage (AWS S3, Cloudinary, etc.)

## Alternative Deployment Options

### Docker Deployment
```bash
# Build image
docker build -t videohub .

# Run container
docker run -p 5000:5000 -e DATABASE_URL=your_db_url videohub
```

### Manual Server Deployment
```bash
# Install dependencies
npm install

# Build application
npm run build

# Set environment variables
export DATABASE_URL=your_postgresql_connection_string
export NODE_ENV=production

# Run migrations
npm run db:push

# Start application
npm start
```

## Production Considerations

### Database
- PostgreSQL 16 is recommended
- Connection pooling is configured automatically
- SSL is enabled for production environments

### File Storage
- Videos and thumbnails are stored locally in `/uploads`
- Consider CDN integration for better performance
- Implement file cleanup for deleted videos

### Security
- HTTPS is handled by Render automatically
- Database connections use SSL in production
- File uploads are validated by type and size

### Performance
- Videos are served with range request support
- Thumbnails are cached by browsers
- Database queries are optimized with indexes

## Troubleshooting

### Common Issues
1. **Database Connection**: Verify DATABASE_URL is set correctly
2. **File Uploads**: Ensure uploads directory exists and is writable
3. **Video Playback**: Check file permissions and video formats
4. **Build Errors**: Verify all dependencies are installed

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `NODE_ENV`: Set to "production" for production deployment
- `PORT`: Port number (defaults to 5000)

### Health Check
The application responds to GET requests on the root path (/) for health checks.