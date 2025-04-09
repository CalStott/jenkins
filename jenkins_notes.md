# Jenkins

### ✅ **Pros of Jenkins**

**1. Open Source & Free**

* Completely free to use, with strong community support and regular updates.

**2. Highly Customisable**

* Supports 1,800+ plugins for integrating with virtually any tool (e.g., GitHub, Docker, Kubernetes, Slack).

**3. Platform Independent**

* Runs on Windows, macOS, and Linux. You can also run it in a container (e.g., Docker) or in the cloud.

**4. Strong Support for CI/CD Pipelines**

* Supports complex workflows via Jenkins Pipelines (written in Groovy) and also simpler freestyle jobs.

**5. Large Community**

* Lots of documentation, tutorials, and forums for support.

**6. Scalable**

* Can distribute builds across multiple machines (master-agent architecture) to speed up large builds and tests.

**7. Active Ecosystem**

* Easily integrates with popular development, testing, and deployment tools.

* * *

### ❌ **Cons of Jenkins**

**1. Steep Learning Curve**

* Especially when dealing with scripted pipelines, plugins, and advanced configurations.

**2. UI Can Be Clunky**

* The web interface is dated and not always intuitive, particularly compared to newer CI/CD tools.

**3. Plugin Maintenance**

* Heavy reliance on plugins means frequent updates—and sometimes plugins break or conflict with each other.

**4. Configuration Complexity**

* Setting up and maintaining Jenkins, especially in a large team or enterprise environment, can become complex and time-consuming.

**5. Limited Built-in Analytics**

* Lacks advanced built-in analytics or dashboards without third-party tools or plugins.

**6. Manual Scaling Challenges**

* While Jenkins can be scaled, doing so often requires manual setup (e.g., adding agents, managing load distribution).

## Typical Stages of Jenkins Pipeline:

### 🛠️ **1. Source Control Management (SCM)**

* **Purpose**: Pull the latest code from a version control system (e.g. Git).

### 🔧 **2. Build**

* **Purpose**: Compile the code or assemble application packages (e.g. JARs, Docker images).
  
* **Typical tools**: Maven, Gradle, npm, Docker
  

### 🧪 **3. Test**

* **Purpose**: Run automated tests—unit, integration, or end-to-end.
  
* **Types**: Unit tests (quick), integration tests (slower), UI tests (slower still)
  

### 📦 **4. Package (optional)**

* **Purpose**: Bundle the application in a deployable format (e.g. .jar, .zip, Docker image).

### 🚀 **5. Deploy**

* **Purpose**: Deploy to a test, staging, or production environment.

### 📊 **6. Monitor**

* **Purpose**:Verify that the deployed application is up, healthy, and behaving as expected. This might include:
  

* Health checks (e.g. hitting `/health` endpoint)
  
* Service availability checks
  
* Smoke tests
  
* Integration with monitoring tools (e.g. Prometheus, Datadog, New Relic)