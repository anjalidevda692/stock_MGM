# 🏪 स्टोर मैनेजमेंट - Spring Boot API

## 📋 प्रोजेक्ट स्ट्रक्चर/Project Structure

```
src/main/java/com/example/store_management/
├── AuthController.java          # Authentication & Authorization
├── ProductController.java       # Product CRUD Operations
├── JwtUtil.java                # JWT Token Generation & Validation
├── SecurityConfig.java         # Spring Security Configuration
├── StoreManagementApplication.java  # Main Application Class
│
├── model/
│   ├── User.java              # User Entity
│   └── Product.java           # Product Entity
│
├── repository/
│   ├── UserRepository.java    # User JPA Repository
│   └── ProductRepository.java # Product JPA Repository
│
└── dto/
    ├── SignUpRequest.java     # Sign-up Form DTO
    ├── SignUpResponse.java    # Sign-up Response DTO
    └── LoginResponse.java     # Login Response DTO

src/main/resources/static/
├── signup.html                # Sign-up Form (हिंदी)
├── login.html                 # Login Form (हिंदी)
└── dashboard.html             # User Dashboard (हिंदी)
```

## 🔐 API Endpoints

### Authentication Endpoints

#### 1. Sign Up (साइन अप)
**URL:** `POST http://localhost:8080/auth/signup`

**Request Body:**
```json
{
  "fullName": "अंजली देवड़ा",
  "username": "anjali_devda",
  "email": "anjali@example.com",
  "password": "password123",
  "confirmPassword": "password123"
}
```

**Response (Success):**
```json
{
  "success": true,
  "message": "उपयोगकर्ता सफलतापूर्वक पंजीकृत",
  "userId": "1"
}
```

#### 2. Login (लॉगिन)
**URL:** `POST http://localhost:8080/auth/login?username=admin&password=1234`

**Response (Success):**
```json
{
  "success": true,
  "message": "सफलतापूर्वक लॉगिन हो गए",
  "token": "eyJhbGciOiJIUzI1NiJ9..."
}
```

### Product Endpoints

#### 1. Get All Products (सभी उत्पाद प्राप्त करें)
**URL:** `GET http://localhost:8080/api/products`

**Response:**
```json
[
  {
    "id": 1,
    "name": "लैपटॉप",
    "description": "उच्च प्रदर्शन लैपटॉप",
    "price": 50000,
    "quantity": 10,
    "createdAt": 1711404000000,
    "updatedAt": 1711404000000
  }
]
```

#### 2. Get Product by ID (ID से उत्पाद प्राप्त करें)
**URL:** `GET http://localhost:8080/api/products/1`

#### 3. Create Product (उत्पाद बनाएं)
**URL:** `POST http://localhost:8080/api/products`

**Request Body:**
```json
{
  "name": "स्मार्टफोन",
  "description": "नवीनतम स्मार्टफोन",
  "price": 25000,
  "quantity": 20
}
```

#### 4. Update Product (उत्पाद को अपडेट करें)
**URL:** `PUT http://localhost:8080/api/products/1`

**Request Body:**
```json
{
  "name": "स्मार्टफोन Pro",
  "price": 30000,
  "quantity": 15
}
```

#### 5. Delete Product (उत्पाद हटाएं)
**URL:** `DELETE http://localhost:8080/api/products/1`

#### 6. Search Products (उत्पाद खोजें)
**URL:** `GET http://localhost:8080/api/products/search?name=लैपटॉप`

## 🔧 Key Classes

### AuthController.java
```java
@RestController
@RequestMapping("/auth")
public class AuthController {
    - signup()      // नए उपयोगकर्ता को पंजीकृत करता है
    - login()       // उपयोगकर्ता को लॉगिन करता है और JWT टोकन प्रदान करता है
}
```

### ProductController.java
```java
@RestController
@RequestMapping("/api/products")
public class ProductController {
    - getAllProducts()      // सभी उत्पाद प्राप्त करता है
    - getProductById()      // विशिष्ट उत्पाद प्राप्त करता है
    - createProduct()       // नया उत्पाद बनाता है
    - updateProduct()       // उत्पाद को अपडेट करता है
    - deleteProduct()       // उत्पाद हटाता है
    - searchProducts()      // नाम से उत्पाद खोजता है
}
```

### JwtUtil.java
```java
public class JwtUtil {
    - generateToken(username)   // JWT टोकन उत्पन्न करता है
    - validateToken(token)      // JWT टोकन को सत्यापित करता है
}
```

### SecurityConfig.java
```java
@Configuration
public class SecurityConfig {
    - filterChain()     // Spring Security कॉन्फ़िगरेशन
                        // CSRF अक्षम, JWT के लिए अनुमति
}
```

## 📊 Database Schema

### Users Table
```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    email VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    created_at BIGINT NOT NULL
);
```

### Products Table
```sql
CREATE TABLE products (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DOUBLE NOT NULL,
    quantity INT NOT NULL,
    created_at BIGINT NOT NULL,
    updated_at BIGINT
);
```

## 🌐 Frontend Pages

### 1. Sign Up Form (`/signup.html`)
- Full Name, Username, Email, Password
- Client-side & Server-side validation
- Hindi Language Support

### 2. Login Form (`/login.html`)
- Username & Password
- JWT Token Storage
- Redirect to Dashboard

### 3. Dashboard (`/dashboard.html`)
- User Welcome Message
- Product Management Links
- Logout Button

## 🚀 Running the Project

```bash
# Build and run
./mvnw clean spring-boot:run

# Alternative - just run
./mvnw spring-boot:run
```

**Application runs on:** `http://localhost:8080`

## 📝 Example Workflows

### Registration & Login Flow
1. Visit `http://localhost:8080/signup.html`
2. Fill in registration form
3. Submit - User saved to database
4. Redirect to login page
5. Login with credentials
6. JWT token received & stored in localStorage
7. Redirected to dashboard

### Product Management
1. Create: `POST /api/products`
2. Read: `GET /api/products`
3. Update: `PUT /api/products/1`
4. Delete: `DELETE /api/products/1`
5. Search: `GET /api/products/search?name=...`

## ⚠️ Important Notes

1. **Password Encoding:** Currently passwords are stored as plain text. In production, use BCrypt:
   ```java
   @Bean
   public PasswordEncoder passwordEncoder() {
       return new BCryptPasswordEncoder();
   }
   ```

2. **JWT Secret Key:** Update the secret key in JwtUtil.java for production

3. **CORS Configuration:** May need to be configured for cross-origin requests

4. **Database Configuration:** Update `application.properties` for your MySQL database

## 🔑 Test Credentials

**Demo Admin Account:**
- Username: `admin`
- Password: `1234`

## 📚 Technologies Used

- **Framework:** Spring Boot 4.0.4
- **Language:** Java 21
- **Database:** MySQL 8.0.43
- **Security:** Spring Security 6.0+, JWT
- **ORM:** JPA/Hibernate
- **Frontend:** HTML5, CSS3, JavaScript (Vanilla)
- **Language:** Hindi (हिंदी) & English

---

**Happy Coding! 🎉**
