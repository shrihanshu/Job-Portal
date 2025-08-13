# Job Portal - Full Stack Job Board Application

A modern, responsive job portal built with React, Supabase, and Clerk authentication. This application allows job seekers to browse and apply for jobs, while recruiters can post and manage job listings.

## 🚀 Features

### For Job Seekers
- **Browse Jobs**: Search and filter jobs by location, company, and keywords
- **Save Jobs**: Bookmark interesting positions for later review
- **Apply to Jobs**: Submit applications with resume uploads
- **Track Applications**: Monitor application status and responses
- **Company Profiles**: View company information and available positions

### For Recruiters
- **Post Jobs**: Create detailed job listings with requirements
- **Manage Applications**: Review and update application statuses
- **Company Management**: Add and manage company profiles
- **Hiring Status**: Toggle job openings on/off
- **Application Tracking**: Monitor candidate applications

### General Features
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile
- **Dark/Light Theme**: Toggle between themes for better user experience
- **Real-time Updates**: Instant updates using Supabase real-time features
- **Secure Authentication**: Clerk-powered user authentication and management
- **File Uploads**: Resume and company logo uploads with Supabase Storage

## 🛠️ Tech Stack

### Frontend
- **React 18** - Modern React with hooks and functional components
- **Vite** - Fast build tool and development server
- **Tailwind CSS** - Utility-first CSS framework for styling
- **React Router** - Client-side routing
- **React Hook Form** - Form handling with validation
- **Zod** - Schema validation

### Backend & Database
- **Supabase** - Backend-as-a-Service with PostgreSQL
- **PostgreSQL** - Relational database
- **Supabase Storage** - File storage for resumes and logos
- **Row Level Security** - Database security policies

### Authentication & UI
- **Clerk** - User authentication and management
- **Shadcn/ui** - Beautiful, accessible UI components
- **Lucide React** - Icon library
- **React Spinners** - Loading animations

## 📁 Project Structure

```
job-portal/
├── public/                 # Static assets
│   ├── companies/         # Company logos
│   ├── logo.png          # App logo
│   └── banner.jpeg       # Landing page banner
├── src/
│   ├── api/              # API functions
│   │   ├── apiApplication.js
│   │   ├── apiCompanies.js
│   │   └── apiJobs.js
│   ├── components/       # Reusable components
│   │   ├── ui/          # Base UI components
│   │   ├── job-card.jsx
│   │   ├── application-card.jsx
│   │   └── ...
│   ├── hooks/           # Custom React hooks
│   │   └── use-fetch.js
│   ├── layouts/         # Layout components
│   │   └── app-layout.jsx
│   ├── pages/           # Page components
│   │   ├── landing.jsx
│   │   ├── jobListing.jsx
│   │   ├── post-job.jsx
│   │   └── ...
│   ├── utils/           # Utility functions
│   │   └── supabase.js
│   ├── App.jsx          # Main app component
│   └── main.jsx         # App entry point
├── package.json
├── tailwind.config.js
└── vite.config.js
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn
- Supabase account
- Clerk account

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd job-portal
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Environment Setup**
   Create a `.env` file in the root directory:
   ```env
   VITE_SUPABASE_URL=your_supabase_project_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
   ```

4. **Database Setup**
   - Create a new Supabase project
   - Run the following SQL to create tables:

   ```sql
   -- Companies table
   CREATE TABLE companies (
     id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
     name TEXT NOT NULL,
     logo_url TEXT,
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );

   -- Jobs table
   CREATE TABLE jobs (
     id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
     title TEXT NOT NULL,
     description TEXT,
     requirements TEXT,
     location TEXT,
     salary_min INTEGER,
     salary_max INTEGER,
     company_id UUID REFERENCES companies(id),
     recruiter_id TEXT NOT NULL,
     isOpen BOOLEAN DEFAULT true,
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );

   -- Applications table
   CREATE TABLE applications (
     id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
     job_id UUID REFERENCES jobs(id),
     candidate_id TEXT NOT NULL,
     name TEXT NOT NULL,
     email TEXT NOT NULL,
     resume TEXT,
     status TEXT DEFAULT 'applied',
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );

   -- Saved Jobs table
   CREATE TABLE saved_jobs (
     id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
     user_id TEXT NOT NULL,
     job_id UUID REFERENCES jobs(id),
     created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
   );
   ```

5. **Storage Setup**
   - Create storage buckets in Supabase:
     - `resumes` - for job application resumes
     - `company-logo` - for company logos
   - Set appropriate RLS policies

6. **Start the development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

7. **Open your browser**
   Navigate to `http://localhost:5173`

## 🔧 Configuration

### Supabase Configuration
- Enable Row Level Security (RLS) on all tables
- Configure storage policies for file uploads
- Set up real-time subscriptions if needed

### Clerk Configuration
- Configure authentication providers
- Set up user roles and permissions
- Configure redirect URLs

### Tailwind Configuration
- Custom color schemes
- Responsive breakpoints
- Component-specific styles

## 📱 Usage

### Job Seeker Workflow
1. **Browse Jobs**: Visit the job listing page to see available positions
2. **Search & Filter**: Use search bar and filters to find relevant jobs
3. **Save Jobs**: Click the save button to bookmark interesting positions
4. **Apply**: Click "Apply Now" to submit an application with resume
5. **Track**: Monitor application status in your applications dashboard

### Recruiter Workflow
1. **Post Job**: Use the "Post Job" form to create new job listings
2. **Manage**: View and edit your posted jobs
3. **Review Applications**: Check incoming applications and update statuses
4. **Company Profile**: Add and manage company information

## 🎨 Customization

### Styling
- Modify `tailwind.config.js` for theme customization
- Update component styles in individual component files
- Customize UI components in the `components/ui` directory

### Features
- Add new job categories or filters
- Implement email notifications
- Add analytics and reporting
- Integrate with external job boards

## 🚀 Deployment

### Vercel (Recommended)
1. Connect your GitHub repository to Vercel
2. Set environment variables in Vercel dashboard
3. Deploy automatically on push to main branch

### Other Platforms
- **Netlify**: Similar to Vercel setup
- **AWS Amplify**: For AWS ecosystem
- **Heroku**: Traditional hosting platform

## 🔒 Security

- **Row Level Security**: Database-level access control
- **Authentication**: Clerk-powered user management
- **File Uploads**: Secure file storage with Supabase
- **Environment Variables**: Sensitive data protection

## 🧪 Testing

```bash
# Run tests
npm run test

# Run tests in watch mode
npm run test:watch

# Generate coverage report
npm run test:coverage
```

## 📊 Performance

- **Code Splitting**: Route-based code splitting
- **Lazy Loading**: Component lazy loading for better performance
- **Image Optimization**: Optimized image loading
- **Bundle Analysis**: Use `npm run build --analyze` for bundle analysis

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Supabase** for the excellent backend service
- **Clerk** for authentication solutions
- **Shadcn/ui** for beautiful UI components
- **Tailwind CSS** for the utility-first CSS framework
- **React Team** for the amazing frontend library

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/yourusername/job-portal/issues) page
2. Create a new issue with detailed information
3. Contact the development team

## 🔄 Changelog

### Version 1.0.0
- Initial release
- Core job portal functionality
- User authentication
- Job posting and application system
- Responsive design

---

**Built with ❤️ using modern web technologies**
