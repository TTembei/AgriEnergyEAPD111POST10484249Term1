# Agri-Energy Connect 🌱⚡

Agri-Energy Connect is a web application designed to bridge the gap between agriculture and green energy. It empowers farmers and employees to collaborate, share resources, and promote sustainable practices through a user-friendly online platform.

---

## 🌟 Features

### 1. User Management
- Role-based authentication (Farmers and Employees)
- Secure user registration and login
- Profile management
- Role-specific dashboards

### 2. Product Management
- Add, edit, and delete products
- Categorized product listings
- Product type filtering
- Search functionality
- Image upload support

### 3. Categories and Product Types
- Predefined categories for better organization
- Dynamic product type filtering
- Easy navigation and search

### 4. User Interface
- Modern, responsive design
- Bootstrap-based layout
- Interactive carousel on homepage
- Role-based navigation
- Sticky footer

## 🛠️ Technology Stack

- **Framework:** ASP.NET Core
- **Database:** SQL Server
- **Authentication:** ASP.NET Core Identity
- **Frontend:** 
  - Bootstrap
  - JavaScript
  - jQuery
  - Font Awesome
- **ORM:** Entity Framework Core

## 📋 Prerequisites

- .NET 7.0 SDK or later
- SQL Server
- Visual Studio 2022 or Visual Studio Code
- Git

## 🚀 Getting Started

### 1. 🚀 Step-by-Step Setup Instructions

#### Prerequisites
- **.NET 7.0 SDK or later** ([Download here](https://dotnet.microsoft.com/download))
- **SQL Server** (Express or full version)
- **Visual Studio 2022** or **Visual Studio Code**
- **Git** (for version control)

#### Setup Steps
1. **Clone the Repository**
   ```bash
   git clone [your-repository-url]
   cd AgriEnergyEAPD111POST10484249Term1/AgriEnergyEAPD111POST10484249Term1
   ```

2. **Configure the Database**
   - Open `appsettings.json` and update the `DefaultConnection` string to point to your SQL Server instance.

3. **Restore Dependencies**
   ```bash
   dotnet restore
   ```

4. **Apply Database Migrations**
   ```bash
   dotnet ef database update
   ```
   > If you do not have the EF Core tools, install them with:
   > ```bash
   > dotnet tool install --global dotnet-ef
   > ```

5. **Build the Project**
   ```bash
   dotnet build
   ```

6. **Run the Application**
   ```bash
   dotnet run
   ```
   - The app will be available at `https://localhost:5001` or `http://localhost:5000`.

### 2. 🛠️ How to Build and Run the Prototype

- **Build:**
  - Use `dotnet build` to compile the project and check for errors.
- **Run:**
  - Use `dotnet run` to start the web server.
- **Access:**
  - Open your browser and go to the local address shown in the terminal (usually `https://localhost:5001`).
- **Stop:**
  - Press `Ctrl+C` in the terminal to stop the application.

### 3. 📖 System Functionalities & User Roles

#### System Functionalities
- **User Authentication:**
  - Secure login and registration using ASP.NET Identity.
- **Role-Based Access:**
  - Two main roles: **Farmer** and **Employee**.
- **Product Management:**
  - Farmers can add, edit, and view their products.
  - Products are categorized and typed for easy browsing.
- **Category & Product Type Management:**
  - Products are organized by category and type for better search and filtering.
- **Collaboration & Marketplace:**
  - Employees can view all products and add new farmers.
  - The platform encourages sharing of sustainable farming and green energy resources.
- **Validation & Error Handling:**
  - All user input is validated for accuracy and completeness.
  - The system provides clear error messages and prevents invalid data from being saved.
- **Responsive Design:**
  - The interface is mobile-friendly and works on all modern browsers.

#### User Roles

##### 👩‍🌾 Farmer
- Register and log in to the platform.
- Add new products with details like name, category, type, production date, and description.
- Edit or update their own products.
- View a list of their products.

##### 🧑‍💼 Employee
- Register and log in to the platform.
- Add new farmers to the system.
- View all products in the marketplace.
- Manage product categories and types.
- Oversee platform activity and support farmers.

### 4. ℹ️ Accessibility & Clarity

- This documentation is written for both technical and non-technical users.
- **Technical users** can follow the setup and build instructions to get the system running locally.
- **Non-technical stakeholders** can review the functionalities and user roles to understand the platform's value and capabilities.
- If you have any questions or need support, please open an issue in the repository or contact the project maintainer.

---

**Agri-Energy Connect** is built to foster collaboration, sustainability, and innovation in agriculture and green energy. Thank you for being part of this journey!

## 🔒 Security Features

- Password hashing
- Role-based authorization
- Secure authentication
- Protected routes
- Input validation

## 📱 Responsive Design

- Mobile-friendly interface
- Adaptive layouts
- Touch-friendly controls
- Cross-browser compatibility

## 🎨 UI Components

- Bootstrap carousel
- Custom navigation bar
- Role-based menus
- Product cards
- Search filters
- Image upload interface

## 🔄 Database Schema

The application uses the following main entities:
- Users (ASP.NET Identity)
- Products
- Categories
- ProductTypes

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

[Your Name]

## 🙏 Acknowledgments

- ASP.NET Core Team
- Bootstrap Team
- Font Awesome
- All contributors and supporters

## 🛡️ Validation & Exception Handling

### 1. Validation Setup

#### a. Data Annotations (Model-Level)
- The `Product` model uses attributes like `[Required]`, `[StringLength]`, etc. for basic validation.
- Example:
  ```csharp
  [Required]
  [StringLength(200)]
  public string Name { get; set; }
  ```

#### b. FluentValidation (Business/Custom Validation)
- **FluentValidation** is used for advanced and business-rule validation.
- The `ProductValidator` class (in `Validators/ProductValidator.cs`) defines rules for the `Product` model.
- Example rules:
  - Name must not be empty and max 200 chars.
  - Category and ProductType must exist in the database.
  - ProductType must belong to the selected Category.
  - ProductionDate cannot be in the future.
  - FarmerId must exist in the users table.

- The validator is registered in `Program.cs`:
  ```csharp
  builder.Services.AddScoped<IValidator<Product>, ProductValidator>();
  ```
- When a product is created or edited, the validator checks the rules before saving to the database.
- If validation fails, errors are added to `ModelState` and shown to the user.

### 2. Exception Handling Setup

#### a. Custom Middleware
- A custom middleware (`Middleware/ExceptionHandlingMiddleware.cs`) catches unhandled exceptions globally.
- It logs the error and returns a structured JSON error response.
- Registered in `Program.cs`:
  ```csharp
  app.UseMiddleware<ExceptionHandlingMiddleware>();
  ```
- Handles:
  - **ValidationException**: Returns 400 with validation errors.
  - **DatabaseOperationException**: Returns 400 with DB error details.
  - **UnauthorizedAccessException**: Returns 401.
  - **KeyNotFoundException**: Returns 404.
  - **Other exceptions**: Returns 500 (Internal Server Error).

#### b. Custom Exceptions
- `ValidationException`: Used for validation errors (from FluentValidation or manual checks).
- `DatabaseOperationException`: Used for database-related errors (e.g., constraint violations).

### 3. Controller Integration
- In controllers (e.g., `ProductController`), validation is performed before any database operation.
- If validation fails, a `ValidationException` is thrown.
- If a database error occurs, a `DatabaseOperationException` is thrown.
- The middleware catches these and returns a user-friendly error response.

### 4. Error Response Example

If a validation error occurs, the API returns:
```json
{
  "message": "Validation Error",
  "details": "One or more validation errors occurred.",
  "errors": {
    "Name": ["Name is required"],
    "ProductionDate": ["Production date cannot be in the future"]
  }
}
```

If a database error occurs:
```json
{
  "message": "Database Error: create product",
  "details": "A product with this information already exists.",
  "entityId": "123"
}
```

### 5. Summary of the Flow

1. **User submits data** (e.g., create/edit product).
2. **FluentValidation** checks business rules.
3. **Data annotations** check basic model rules.
4. If validation fails, a `ValidationException` is thrown.
5. If a DB error occurs, a `DatabaseOperationException` is thrown.
6. **ExceptionHandlingMiddleware** catches exceptions and returns a structured error response.

**This setup ensures:**
- Data is always validated before saving.
- Users get clear, actionable error messages.
- The system is robust against crashes and data corruption.

---

For any questions or support, please open an issue in the repository. 
