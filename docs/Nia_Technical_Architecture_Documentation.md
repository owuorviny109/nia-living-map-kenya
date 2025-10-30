# Nia: The Living Map of Kenya
## Technical Architecture & Services Documentation

---

## 📋 **Executive Summary**

Nia is an AI-powered exploration platform that reimagines how travelers experience Kenya. Built as a Progressive Web App (PWA) using Django and AWS free-tier services, it creates a living, narrative-driven map that blends geography, culture, and live data.

**Cost**: $0/month FOREVER - 100% AWS Free Tier Only

---

## 🎯 **Project Vision**

To make Kenya legible and alive — a single intelligent map that understands where, why, and when to go.

*"Not just what's there, but what's happening, what it costs, and what it means."*

---

## 🏗️ **Architecture Overview**

### **Core Technology Stack**
- **Backend**: Django 4.2.7 (Python web framework)
- **Frontend**: Bootstrap 5 + Django Templates
- **Database**: PostgreSQL (RDS free tier)
- **Cloud**: AWS Free Tier Services
- **AI**: 100% Free AI (AWS Comprehend, Hugging Face, Local Processing)

### **Deployment Architecture**
```
Internet → Route 53 → EC2 (Django) → RDS (PostgreSQL)
                           ↓
                    S3 (Stories/Images) ← Lambda (AI Processing)
```

---

## 🔧 **Django Built-in Services Used**

### **Authentication & User Management**
- **User Model**: Built-in user registration, login, logout
- **Permissions**: User groups and role-based access
- **Password Reset**: Email-based password recovery
- **Social Auth**: Google/Facebook login integration
- **Sessions**: User session management

### **Database & ORM**
- **Models**: Database abstraction for destinations, stories, users
- **Migrations**: Automatic database schema management
- **QuerySets**: Optimized database queries
- **Admin Interface**: Auto-generated content management system

### **Web Framework Features**
- **Views**: Class-based and function-based views
- **Templates**: HTML templating with inheritance
- **Forms**: Form handling and validation
- **URL Routing**: Clean URL patterns
- **Static Files**: CSS/JS/images handling
- **Middleware**: Request/response processing

### **Security (Built-in)**
- **CSRF Protection**: Cross-site request forgery prevention
- **XSS Protection**: Cross-site scripting prevention
- **SQL Injection Protection**: ORM prevents SQL injection
- **Clickjacking Protection**: X-Frame-Options header
- **HTTPS Redirect**: Force secure connections

### **Utilities**
- **Email Backend**: Send notifications and alerts
- **File Uploads**: Handle story images and audio
- **Pagination**: Split large datasets efficiently
- **Caching Framework**: In-memory and database caching
- **Internationalization**: English/Swahili support
- **Time Zones**: Timezone-aware datetime handling

---

## ☁️ **AWS Free Tier Services**

### **Core Infrastructure (Always Free)**
| Service | Free Tier Limit | Usage in Nia |
|---------|----------------|--------------|
| **EC2 t2.micro** | 750 hours/month | Django application server |
| **RDS PostgreSQL t3.micro** | 750 hours/month, 20GB | Main database |
| **S3** | 5GB storage, 20K GET requests | Static files, story content |
| **CloudWatch** | 10 custom metrics | Basic monitoring & logging |
| **IAM** | Unlimited | User & permission management |
| **VPC** | Unlimited | Network isolation |

### **Serverless & Processing**
| Service | Free Tier Limit | Usage in Nia |
|---------|----------------|--------------|
| **Lambda** | 1M requests/month | AI processing, background tasks |
| **API Gateway** | 1M requests/month | REST APIs for mobile app |
| **SQS** | 1M requests/month | Message queues for async tasks |
| **SNS** | 1M publishes/month | Push notifications |
| **EventBridge** | Unlimited | Scheduled data updates |

### **AI & ML Services**
| Service | Free Tier Limit | Usage in Nia |
|---------|----------------|--------------|
| ~~Comprehend~~ | REMOVED | Too expensive after free tier |
| ~~Translate~~ | REMOVED | Too expensive after free tier |
| ~~Polly~~ | REMOVED | Too expensive after free tier |

### **Content Delivery**
| Service | Free Tier Limit | Usage in Nia |
|---------|----------------|--------------|
| **CloudFront** | 50GB data transfer/month | CDN for static assets |
| **Route 53** | 1 hosted zone | DNS management |
| **Certificate Manager** | Unlimited | Free SSL certificates |

---

## 🤖 **100% Free AI Integration**

### **Primary AI Services (Zero Cost)**
1. **Hugging Face Transformers**
   - **Cost**: Completely FREE (local processing)
   - **Usage**: All AI features - text analysis, sentiment, translation, summarization
   - **Integration**: Django management commands + background tasks
   - **Models**: 
     - Text classification (story moderation)
     - Sentiment analysis (user feedback)
     - Summarization (destination summaries)
     - Translation (English/Swahili)
     - Named Entity Recognition (location extraction)

### **Local AI Processing Benefits**
- **Zero API Costs**: No external API calls
- **Privacy**: All data stays on your server
- **Offline Capable**: Works without internet
- **Customizable**: Fine-tune models for Kenya-specific content
- **Scalable**: Runs on EC2 free tier

### **AI Features Implementation (Hugging Face Only)**
- **Story Moderation**: Text classification models for content filtering
- **Sentiment Analysis**: User review sentiment scoring
- **Content Summarization**: Auto-generate destination summaries
- **Translation**: English/Swahili translation models
- **Location Extraction**: NER models for place name recognition
- **Recommendation Engine**: Content-based filtering using embeddings

---

## 📱 **Application Features (Based on UI Mockups)**

### **1. Navigation & Core Pages**
- **Home Page**: Interactive map with AI-powered itinerary builder
- **Discover Page**: Filterable destination grid with comparison tool
- **Stories Page**: Community-contributed stories with map integration
- **Destination Detail**: Comprehensive location information
- **Contribute Page**: Story and media upload interface

### **2. User Authentication**
- **Login Page**: Email/password + social auth (Google/Facebook)
- **Sign Up Page**: User registration with terms acceptance
- **Password Reset**: Email-based recovery system
- **User Profile**: Account management and preferences

### **3. Interactive Features**
- **Map Integration**: Leaflet.js with OpenStreetMap data
- **Search & Filters**: County, experience type, budget filters
- **Story Upload**: Text, image, and audio content submission
- **AI Itinerary Builder**: Personalized trip recommendations
- **Comparison Tool**: Side-by-side destination comparison

### **4. Content Management**
- **Admin Interface**: Django admin for content moderation
- **Story Moderation**: AI-assisted content review
- **Local Business Directory**: Community-driven listings
- **Event Management**: Live events and updates

---

## 🗄️ **Database Schema**

### **Core Models**
```python
# User Management
User (Django built-in)
UserProfile (extends User)

# Geographic Data
County
Destination
Location (GPS coordinates)

# Content
Story
StoryMedia (images/audio)
LocalBusiness
Event

# AI Features
AIInsight
RealnessScore
TripItinerary
```

### **Key Relationships**
- Users can create multiple Stories
- Destinations belong to Counties
- Stories are linked to Destinations
- AI Insights are generated for Destinations
- Trip Itineraries contain multiple Destinations

---

## 🚀 **Deployment Strategy**

### **Development Environment**
- **Local**: SQLite database, Django dev server
- **Static Files**: Local file system
- **AI Processing**: Local API calls

### **Production Environment**
- **Application**: EC2 t2.micro with Gunicorn + Nginx
- **Database**: RDS PostgreSQL t3.micro
- **Static Files**: S3 + CloudFront CDN
- **Background Tasks**: Lambda functions
- **Monitoring**: CloudWatch logs and metrics

### **CI/CD Pipeline**
- **Version Control**: Git repository
- **Deployment**: Manual deployment initially
- **Future**: AWS CodePipeline for automated deployments

---

## 📊 **Performance Optimization**

### **Django Optimizations**
- **Database**: Query optimization with select_related/prefetch_related
- **Caching**: Redis caching for frequently accessed data
- **Static Files**: WhiteNoise for efficient static file serving
- **Templates**: Template fragment caching

### **AWS Optimizations**
- **CDN**: CloudFront for global content delivery
- **Database**: Connection pooling and read replicas
- **Lambda**: Efficient function design for quick execution
- **S3**: Optimized file storage and retrieval

---

## 🔒 **Security Implementation**

### **Django Security**
- **CSRF Protection**: Enabled by default
- **XSS Prevention**: Template auto-escaping
- **SQL Injection**: ORM prevents direct SQL
- **Secure Headers**: Security middleware enabled
- **HTTPS**: SSL/TLS encryption enforced

### **AWS Security**
- **IAM**: Least privilege access policies
- **VPC**: Network isolation and security groups
- **S3**: Bucket policies and access controls
- **RDS**: Encrypted storage and secure connections

---

## 📈 **Scalability Plan**

### **Phase 1: MVP (Free Tier)**
- Single EC2 instance
- Basic RDS setup
- Simple S3 storage
- Manual content moderation

### **Phase 2: Growth**
- Auto Scaling Groups
- RDS Multi-AZ deployment
- Advanced AI features
- Automated content moderation

### **Phase 3: Scale**
- Multiple regions
- Advanced caching strategies
- Machine learning pipelines
- Mobile app development

---

## 🛠️ **Development Workflow**

### **Local Development Setup**
1. Clone repository
2. Create virtual environment
3. Install requirements.txt
4. Run Django migrations
5. Load sample data
6. Start development server

### **Key Commands**
```bash
# Setup
python -m venv venv
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver

# Deployment
python manage.py collectstatic
python manage.py migrate --settings=production
gunicorn nia.wsgi:application
```

---

## 💰 **Cost Analysis**

### **Year 1 (Free Tier)**
- **Total Cost**: $0/month
- **Services**: All within free tier limits
- **Estimated Usage**: 1000 users, 10K page views/month

### **Always Free Architecture**
- **EC2**: FREE (750 hours/month t2.micro)
- **RDS**: FREE (750 hours/month t3.micro, 20GB)
- **S3**: FREE (5GB storage, 20K requests)
- **Lambda**: FREE (1M requests/month)
- **Total**: $0/month FOREVER within limits

---

## 🎯 **Success Metrics**

### **Technical Metrics**
- **Uptime**: >99.5%
- **Page Load Time**: <3 seconds
- **API Response Time**: <500ms
- **Error Rate**: <1%

### **Business Metrics**
- **User Registration**: Growth rate
- **Story Contributions**: Community engagement
- **Destination Views**: Content popularity
- **AI Usage**: Feature adoption

---

## 🔄 **Maintenance & Updates**

### **Regular Tasks**
- **Security Updates**: Monthly Django/dependency updates
- **Database Maintenance**: Weekly backups and optimization
- **Content Moderation**: Daily story review
- **Performance Monitoring**: Continuous CloudWatch monitoring

### **Feature Updates**
- **AI Model Updates**: Quarterly improvements
- **UI Enhancements**: Based on user feedback
- **New Destinations**: Monthly content additions
- **API Improvements**: Ongoing optimization

---

## 📚 **Documentation & Resources**

### **Technical Documentation**
- **API Documentation**: Django REST framework docs
- **Database Schema**: ER diagrams and model documentation
- **Deployment Guide**: Step-by-step AWS setup
- **Development Guide**: Local setup and contribution guidelines

### **User Documentation**
- **User Manual**: How to use Nia features
- **Content Guidelines**: Story submission guidelines
- **FAQ**: Common questions and troubleshooting
- **Community Guidelines**: Platform rules and etiquette

---

## 🏢 **AWS Well-Architected Framework - 6 Pillars**

### **1. Operational Excellence**
- **Monitoring**: CloudWatch logs and metrics (free tier)
- **Automation**: Lambda functions for background tasks
- **Documentation**: Comprehensive technical docs
- **Deployment**: Infrastructure as Code with Terraform

### **2. Security**
- **Identity**: IAM roles with least privilege
- **Data Protection**: RDS encryption, S3 bucket policies
- **Network**: VPC with security groups
- **Application**: Django built-in security features

### **3. Reliability**
- **Fault Tolerance**: Multi-AZ RDS deployment
- **Backup**: Automated RDS backups
- **Monitoring**: CloudWatch alarms
- **Recovery**: Disaster recovery procedures

### **4. Performance Efficiency**
- **Compute**: Right-sized EC2 t2.micro
- **Storage**: S3 for static files with CloudFront CDN
- **Database**: Optimized PostgreSQL queries
- **Caching**: Django caching framework

### **5. Cost Optimization**
- **Resource Management**: 100% free tier services
- **Monitoring**: Cost tracking with AWS Budgets
- **Right Sizing**: Efficient resource allocation
- **Reserved Capacity**: Plan for future growth

### **6. Sustainability**
- **Efficient Code**: Optimized Django applications
- **Resource Utilization**: Serverless Lambda functions
- **Data Management**: Efficient S3 storage patterns
- **Green Computing**: AWS's renewable energy commitment

---

## 🎉 **Conclusion**

Nia leverages Django's robust built-in features combined with 100% AWS free-tier services to create a powerful, scalable platform for exploring Kenya. The architecture follows AWS Well-Architected Framework principles while maintaining ZERO cost.

The combination of Django's "batteries included" philosophy and AWS's comprehensive free tier makes this project both technically sound and financially sustainable forever.

**Total Cost: $0/month - GUARANTEED**

---

**Generated**: January 2025  
**Version**: 2.0  
**Status**: 100% Free Tier Architecture