# VideoHub - Video Sharing Platform

A full-stack video sharing platform built with React, Express, and PostgreSQL. Features video recording, upload, streaming, and management capabilities.

## Features

- **Video Recording**: WebRTC-based video recording with webcam
- **Video Upload**: Support for MP4, WebM, AVI, and MOV formats
- **Video Streaming**: Optimized video playback with range request support
- **Thumbnail Generation**: Automatic thumbnail capture from video frames
- **Responsive Design**: Mobile-friendly interface with Tailwind CSS
- **Admin Panel**: Hidden admin access for content management
- **Database**: PostgreSQL with Drizzle ORM for type-safe operations

## Tech Stack

### Frontend
- React 18 with TypeScript
- Tailwind CSS + shadcn/ui components
- Wouter for routing
- TanStack Query for state management
- Vite for build tooling

### Backend
- Node.js + Express
- PostgreSQL 16 database
- Drizzle ORM with migrations
- Multer for file uploads
- Video streaming with range requests

## Quick Start

### Development
```bash
# Install dependencies
npm install

# Start development server
npm run dev
```

### Production Deployment

#### Render.com (Recommended)
1. Create PostgreSQL 16 database on Render
2. Deploy using the provided `render.yaml` configuration
3. Set `DATABASE_URL` environment variable
4. Application will auto-build and deploy

#### Docker
```bash
# Build and run
docker build -t videohub .
docker run -p 5000:5000 -e DATABASE_URL=your_db_url videohub
```

#### Manual Server
```bash
# Build application
npm run build

# Set environment variables
export DATABASE_URL=your_postgresql_connection_string
export NODE_ENV=production

# Run database migrations
npm run db:push

# Start server
npm start
```

## Environment Variables

```env
DATABASE_URL=postgresql://username:password@localhost:5432/videohub
NODE_ENV=development
PORT=5000
```

## API Endpoints

- `GET /` - Health check
- `GET /api/videos` - List all videos
- `GET /api/videos/:id` - Get video details
- `POST /api/videos` - Upload video
- `POST /api/videos/:id/view` - Increment view count
- `DELETE /api/videos/:id` - Delete video
- `GET /uploads/videos/:filename` - Stream video files
- `GET /uploads/thumbnails/:filename` - Serve thumbnails

## File Structure

```
├── client/              # React frontend
│   ├── src/
│   │   ├── components/  # Reusable components
│   │   ├── pages/       # Route pages
│   │   └── lib/         # Utilities
├── server/              # Express backend
│   ├── index.ts         # Server entry point
│   ├── routes.ts        # API routes
│   ├── db.ts            # Database configuration
│   └── storage.ts       # Data access layer
├── shared/              # Shared types and schemas
├── uploads/             # File storage
│   ├── videos/          # Video files
│   └── thumbnails/      # Thumbnail images
├── render.yaml          # Render deployment config
├── Dockerfile           # Docker configuration
└── DEPLOYMENT.md        # Detailed deployment guide
```

## Features Overview

### Admin Panel
- Access via small gear icon on homepage
- Video recording with webcam
- Upload videos with metadata
- Real-time recording preview
- Thumbnail capture from video frames

### Video Streaming
- Range request support for smooth playback
- Multiple format support (MP4, WebM, AVI, MOV)
- Automatic content-type detection
- Optimized for mobile and desktop

### Database Schema
- Users table for future authentication
- Videos table with metadata, views, and file paths
- Proper indexes for performance
- Type-safe operations with Drizzle ORM

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

MIT License - feel free to use this project for your own purposes.

## Support

For deployment issues or questions, refer to the detailed [DEPLOYMENT.md](DEPLOYMENT.md) guide.