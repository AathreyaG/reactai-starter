```plantuml
@startuml
!includeurl https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

' Title
title GSA Supply Catalog Management Platform - Backend Architecture (Container Diagram)

' Define the system
System_Boundary(GSA_Boundary, "Supply Catalog Management Platform") {

    ' Users
    Person(user, "GSA Acquisition Workforce", "Interacts with the platform to manage supply catalog")

    ' Frontend Application
    Container(webApp, "Web Application", "React + TypeScript", "User interface for uploading and managing supply catalog data")

    ' API Gateway
    Container(apiGateway, "API Gateway", "Amazon API Gateway", "Handles request routing, validation, and authorization")

    ' Core Backend Services
    Container_Boundary(Backend, "Backend Services") {
        Container(appNode, "Application Server", "Node.js + Express on Elastic Beanstalk", "Processes business logic and data transactions")
        Container(authService, "Authentication Service", "Amazon Cognito", "Manages user authentication and authorization")
        Container(database, "Database", "PostgreSQL on RDS", "Stores supply catalog data securely with relational capabilities")
        Container(fileStorage, "File Storage", "Amazon S3", "Stores uploaded CSV files and provides export storage")
        Container(lambda, "Background Processing", "AWS Lambda", "Executes asynchronous tasks like CSV file validation and processing")
    }

    ' Monitoring and Security
    System_Ext(cloudwatch, "CloudWatch", "AWS CloudWatch", "Monitors application performance and logs")
    System_Ext(secretsManager, "Secrets Manager", "AWS Secrets Manager", "Manages sensitive configurations securely")
    System_Ext(vpc, "Virtual Private Cloud", "AWS VPC", "Isolates backend services in a secure network environment")

    ' Relationships and Flows
    Rel(user, webApp, "Uses", "HTTPS")
    Rel(webApp, apiGateway, "Sends requests to", "HTTPS")
    Rel(apiGateway, appNode, "Routes requests to", "HTTPS")
    Rel(appNode, database, "Reads from and writes to", "JDBC")
    Rel(appNode, fileStorage, "Stores and retrieves files from", "HTTPS")
    Rel(appNode, lambda, "Triggers for background tasks", "HTTPS")
}

' Notes
note right of authService
Utilizes Amazon Cognito for
secure user authentication
and session management
end note

@enduml
```

### Detailed Architecture Explanation:

#### 1. **Frontend Architecture (React + TypeScript)**
- **Component Structure**: 
  - Built using a modular approach, each key feature is a component.
    - **Header Component**: Contains navigation and user actions.
    - **CatalogTable Component**: Displays product catalogs with interactive features like sorting and filtering.
    - **ProductDetail Component**: Displays product information and allows editing, interfacing with backend CRUD APIs.
    - **CSVUploader Component**: For CSV uploads, manages drag-and-drop functionality, upload progress, and error reporting.
    - **ExportComponent**: Utilizes backend endpoints to facilitate CSV export.
- **UI Frameworks/Component Libraries**: 
  - **Material-UI (MUI)** for a comprehensive set of components and theming capabilities.
  - **USWDS Components** to ensure compliance with federal accessibility standards.

#### 2. **Backend Architecture (Node.js + Express + PostgreSQL)**
- **RESTful API Endpoints**:
  - **POST /api/upload**: Handles CSV uploads with validation, storing in S3.
  - **GET /api/products**: Retrieves product data, supporting pagination, sorting, and filtering.
  - **POST /api/products**: Adds new catalog items with necessary validations.
  - **GET/PUT/DELETE /api/products/:id**: Manages individual product data, facilitating retrieval, updates, or deletions.
  - **GET /api/export**: Generates CSV from product data, interacts with S3 for file operations.
- **Data Processing Workflows**:
  - **File Handling**: Uses **Multer** with Express for file upload management.
  - **Validation**: Employs **Joi** for rigorous data validation to ensure integrity.
  - **Background Processing**: Utilizes **AWS Lambda** for asynchronous tasks like CSV parsing, allowing the main application to remain responsive.

#### 3. **AWS Infrastructure & Deployment**
- **Hosting**:
  - **AWS Elastic Beanstalk**: Manages environment provisioning, scaling, and monitoring for Node.js applications.
- **File Storage**:
  - **Amazon S3**: Used for storing raw and processed CSV files, granting durable and scalable storage solutions.
- **Database**:
  - **Amazon RDS (PostgreSQL)**: Offers a managed, scalable, and reliable relational database service.
- **API Management**:
  - **Amazon API Gateway**: Acts as the entry point for API requests, incorporating request validation, and authorization.
- **Security**:
  - **Amazon Cognito**: Provides user identity management and authentication services.
- **CI/CD Pipeline**:
  - **AWS CodePipeline**: Facilitates the automation of build, test, and deployment processes using **AWS CodeBuild** and **CodeDeploy**, ensuring effective CI/CD practices.