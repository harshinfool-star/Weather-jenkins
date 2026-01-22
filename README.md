# Weather Dashboard - Jenkins CI/CD Pipeline Practice

## 📋 Project Overview
This is a simple web application that displays:
- **Live Time**: Real-time clock updated every second
- **Weather Information**: Mock weather data for any city

This project includes a complete Jenkins pipeline for CI/CD practice.

## 🚀 Getting Started

### Prerequisites
- Jenkins installed (download from https://www.jenkins.io/download/)
- Git (for version control)

### Local Testing
1. Open `index.html` directly in your browser
2. The page will display live time and weather information

## 🔧 Jenkins Setup

### Step 1: Install Jenkins (if not already installed)
```bash
# macOS (using Homebrew)
brew install jenkins-lts
brew services start jenkins-lts

# Access Jenkins at: http://localhost:8080
```

### Step 2: Initial Jenkins Configuration
1. Open Jenkins at `http://localhost:8080`
2. Retrieve the initial admin password:
   ```bash
   cat ~/.jenkins/secrets/initialAdminPassword
   ```
3. Install suggested plugins
4. Create your first admin user

### Step 3: Create Your First Pipeline

#### Option A: Pipeline from SCM (Recommended)
1. Click "New Item"
2. Enter name: `weather-dashboard-pipeline`
3. Select "Pipeline" and click OK
4. Under "Pipeline" section:
   - Definition: `Pipeline script from SCM`
   - SCM: `Git`
   - Repository URL: (your git repository URL)
   - Script Path: `Jenkinsfile`
5. Click "Save"

#### Option B: Direct Pipeline Script
1. Click "New Item"
2. Enter name: `weather-dashboard-pipeline`
3. Select "Pipeline" and click OK
4. Under "Pipeline" section:
   - Definition: `Pipeline script`
   - Copy and paste the contents of `Jenkinsfile`
5. Click "Save"

### Step 4: Run Your Pipeline
1. Click "Build Now"
2. Watch the pipeline stages execute:
   - ✅ Checkout
   - ✅ Validate HTML
   - ✅ Run Tests
   - ✅ Build
   - ✅ Deploy to Staging
   - ✅ Approval (auto-approved)
   - ✅ Deploy to Production

## 📊 Pipeline Stages Explained

1. **Checkout**: Gets the code from the repository
2. **Validate HTML**: Checks if required files exist
3. **Run Tests**: Validates HTML content and functionality
4. **Build**: Creates a build directory with the application
5. **Deploy to Staging**: Deploys to staging environment
6. **Approval**: Manual approval gate (auto-approved for demo)
7. **Deploy to Production**: Final production deployment

## 🎯 Learning Objectives

This project helps you learn:
- ✅ Creating a basic Jenkins pipeline
- ✅ Understanding pipeline stages
- ✅ Running automated tests
- ✅ Implementing deployment stages
- ✅ Using post-build actions
- ✅ Archiving build artifacts

## 🔍 Advanced Jenkins Features to Explore

### 1. Add GitHub Integration
```groovy
// In Jenkinsfile, add:
stage('Notify GitHub') {
    steps {
        // Update GitHub commit status
        echo 'Updating GitHub status...'
    }
}
```

### 2. Add Email Notifications
```groovy
post {
    success {
        mail to: 'your-email@example.com',
             subject: "Build Successful: ${env.JOB_NAME}",
             body: "Build ${env.BUILD_NUMBER} completed successfully"
    }
}
```

### 3. Add Scheduled Builds
In Jenkins job configuration, add:
```
Build Triggers > Build periodically
H/15 * * * *  # Build every 15 minutes
```

## 📝 Customization Ideas

1. **Real Weather API**:
   - Sign up at https://openweathermap.org/api
   - Replace the mock data with real API calls
   - Add your API key to Jenkins credentials

2. **Add More Tests**:
   - HTML validation with Nu Html Checker
   - JavaScript linting with ESLint
   - Performance testing

3. **Docker Integration**:
   - Create a Dockerfile
   - Build and push Docker images in the pipeline

4. **Kubernetes Deployment**:
   - Add K8s deployment manifests
   - Deploy to a Kubernetes cluster

## 🐛 Troubleshooting

### Pipeline Fails at Build Stage
- Ensure Jenkins has permission to create directories
- Check workspace permissions

### HTML Not Found Error
- Verify the file exists in the workspace
- Check the repository is cloned correctly

### Jenkins Not Starting
```bash
# Check Jenkins status
brew services list

# Restart Jenkins
brew services restart jenkins-lts
```

## 📚 Additional Resources

- [Jenkins Official Documentation](https://www.jenkins.io/doc/)
- [Jenkins Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)
- [Jenkins Blue Ocean UI](https://www.jenkins.io/doc/book/blueocean/)

## 🎓 Next Steps

1. Set up a Git repository for this project
2. Configure webhooks for automatic builds
3. Add more sophisticated testing
4. Implement proper staging/production environments
5. Explore Jenkins plugins for enhanced functionality

---

**Happy Learning! 🚀**
