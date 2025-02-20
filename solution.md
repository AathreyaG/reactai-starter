### Detailed Explanation of the Proposed Architecture

#### 1. **Frontend Architecture (React + TypeScript)**

- **Component Structure**:
  - The frontend is composed of modular React components to support a scalable and maintainable user interface:
    - **Header Component**: Provides navigation and user-related actions.
    - **CatalogTable Component**: Displays product catalog with interactive features like pagination, sorting, and filtering.
    - **ProductDetail Component**: Enables detailed product view and editing.
    - **CSVUploader Component**: Allows CSV file uploads with drag-and-drop functions.
    - **ExportComponent**: Facilitates downloading catalog data as CSV files.

- **UI Frameworks/Component Libraries**:
  - **Material-UI (MUI)**: Chosen for its comprehensive component library and cohesive visual design.
  - **USWDS Components**: Used to fulfill US federal accessibility requirements and ensure a consistent user experience.

#### 2. **Backend Architecture (Node.js + Express + PostgreSQL)**

- **RESTful API Endpoints**:
  - **/api/upload**:
    - **POST**: Accepts and validates CSV file uploads before storage on S3.
  - **/api/products**:
    - **GET**: Fetches a list of products with options for sorting and filtering.
    - **POST**: Allows adding new products to the catalog.
  - **/api/products/:id**:
    - **GET**: Retrieves details of a specific product.
    - **PUT**: Updates an existing product's details.
    - **DELETE**: Removes a product from the catalog.
  - **/api/export**:
    - **GET**: Triggers the export of product data to a CSV file stored on S3.

- **Data Processing Workflows**:
  - **File Handling**: Utilizes the **Multer** library for efficient handling of file uploads.
  - **Validations**: Ensures data integrity using the **Joi** library for structural validation.
  - **Background Processing**: Leverages **AWS Lambda** for asynchronous tasks like CSV file validation, to optimize performance.

#### 3. **AWS Infrastructure & Deployment**

- **Hosting**:
  - **AWS Elastic Beanstalk**: Automated deployment and scaling of Node.js applications with monitoring.

- **File Storage**:
  - **Amazon S3**: Dedicated to storing both raw and processed CSV files.

- **Database**:
  - **Amazon RDS with PostgreSQL**: Provides a reliable, scalable relational database solution.

- **API Management**:
  - **Amazon API Gateway**: Routes API traffic with integrated security and validation features.

- **Security**:
  - **Amazon Cognito**: Handles user identity management, ensuring secure authentication and authorization.

- **CI/CD Pipeline**:
  - **AWS CodePipeline**: Combined with **CodeBuild** and **CodeDeploy** for a streamlined continuous integration and deployment process, enabling efficient and error-free updates.

## Generated Diagrams

![Diagram 1](./images/solution_diagram_1.png)