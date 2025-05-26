# 🎥 Cinema Information Management System

A professional database management project built to simulate real-world operations at a cinema — inspired by **Cinepax** (Pakistan's leading cinema chain). This comprehensive system models core entities like movies, screens, tickets, food orders, genres, and customers using SQL Server.

## 📌 Features

### 📊 Database Design
- **ER Diagrams** (Abnormal & Normalized)
- **Relational Schema** with proper Primary Keys
- **Normalization** up to 3NF for data integrity
- **Entity Relationships** mapping for complex business logic

### 🏗️ Implementation
- **SQL Table Creation Scripts** for all entities
- **Sample Data Insertion** across 10+ interconnected tables
- **Advanced SQL Queries** utilizing JOIN, LIKE, GROUP BY, aggregation functions
- **Referential Integrity** with foreign key constraints

### 🎯 Core Business Scenarios

#### 🎟️ Ticket Booking System
- Customer registration and login
- Movie selection with showtimes
- Seat availability checking
- Ticket price calculation based on screen type and time
- Booking confirmation and ticket generation

#### 🍿 Food Ordering System
- Menu management with categories
- Order placement during ticket booking
- Price calculation with combo deals
- Kitchen order processing
- Customer receipt generation

#### 🎬 Movie & Content Management
- Movie information with multiple genres
- Rating and certification tracking
- Showtime scheduling across multiple screens
- Duration and language management

#### 🪑 Seat & Screen Allocation
- Multiple screen types (Standard, VIP, IMAX)
- Dynamic seat mapping and availability
- Screen capacity management
- Seat pricing based on location and screen type

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| **Database** | Microsoft SQL Server Management Studio |
| **Design Tool** | Draw.io (for ER Diagrams) |
| **Documentation** | PDF Report with detailed analysis |
| **Query Language** | T-SQL (Transact-SQL) |

## 📁 Project Structure

```
Cinema-Management-System/
├── 📄 CinemaDB_Project_Report.pdf
├── 📝 README.md
├── 🗃️ Database_Scripts/
│   ├── 01_Table_Creation.sql
│   ├── 02_Data_Insertion.sql
│   ├── 03_Sample_Queries.sql
│   └── 04_Stored_Procedures.sql
├── 📊 ER_Diagrams/
│   ├── Conceptual_ERD.drawio
│   ├── Logical_ERD.drawio
│   └── Physical_ERD.drawio
└── 📋 Documentation/
    ├── Database_Schema.md
    ├── Query_Examples.md
    └── Use_Cases.md
```

## 🗂️ Database Schema Overview

### Core Entities

| Table | Description | Key Relationships |
|-------|-------------|------------------|
| **Customers** | Customer information and registration | → Tickets, Food_Orders |
| **Movies** | Movie details, ratings, duration | → Showtimes, Movie_Genres |
| **Genres** | Movie categories (Action, Comedy, etc.) | → Movie_Genres |
| **Screens** | Cinema halls with capacity and type | → Showtimes, Seats |
| **Seats** | Individual seat information | → Tickets, Seat_Types |
| **Showtimes** | Movie schedules across screens | → Tickets |
| **Tickets** | Booking records with pricing | → Customers, Showtimes, Seats |
| **Food_Items** | Menu items with categories | → Order_Items |
| **Food_Orders** | Customer food purchases | → Customers, Order_Items |
| **Staff** | Employee management | → Ticket_Sales, Order_Processing |

### 🔗 Key Relationships
- **One-to-Many**: Customer → Multiple Tickets
- **Many-to-Many**: Movies ↔ Genres (via Movie_Genres)
- **One-to-One**: Ticket → Seat (for specific showtime)
- **Hierarchical**: Screen → Seats → Seat_Types

## 📋 Sample Queries

### 🎫 Popular Movie Analysis
```sql
SELECT 
    m.movie_name,
    COUNT(t.ticket_id) as total_tickets,
    SUM(t.ticket_price) as total_revenue
FROM Movies m
JOIN Showtimes s ON m.movie_id = s.movie_id
JOIN Tickets t ON s.showtime_id = t.showtime_id
GROUP BY m.movie_name
ORDER BY total_tickets DESC;
```

### 🍕 Food Revenue by Category
```sql
SELECT 
    fi.category,
    SUM(oi.quantity * oi.unit_price) as category_revenue
FROM Food_Items fi
JOIN Order_Items oi ON fi.item_id = oi.item_id
GROUP BY fi.category
ORDER BY category_revenue DESC;
```

### 🪑 Screen Utilization Report
```sql
SELECT 
    sc.screen_name,
    sc.capacity,
    COUNT(t.ticket_id) as seats_sold,
    (COUNT(t.ticket_id) * 100.0 / sc.capacity) as utilization_percentage
FROM Screens sc
LEFT JOIN Showtimes sh ON sc.screen_id = sh.screen_id
LEFT JOIN Tickets t ON sh.showtime_id = t.showtime_id
GROUP BY sc.screen_name, sc.capacity
ORDER BY utilization_percentage DESC;
```

## 🎓 Academic Information

| Detail | Information |
|--------|-------------|
| **📚 Course** | Database Systems (CS-2003) |
| **🏫 University** | Government College University, Lahore |
| **🎓 Department** | Computer Science |
| **👩‍💻 Team Members** | Jaweria Fayyaz, Maira Tanveer |
| **📆 Semester** | 4th Semester, BSCS |

## 📄 Documentation

### 📥 Project Report
**[📄 Download Full Report (PDF)](CinemaDB_Project_Report.pdf)**

The comprehensive project report includes:
- **Executive Summary** of the cinema management system
- **Detailed ER Diagrams** (Conceptual, Logical, Physical)
- **Normalization Process** with examples
- **Complete SQL Scripts** for database creation
- **Sample Data** with realistic cinema operations
- **Advanced Queries** with business logic
- **Use Case Scenarios** with step-by-step workflows
- **Performance Analysis** and optimization suggestions

### 📊 Key Sections Covered
1. **Introduction & Scope**
2. **System Requirements Analysis**
3. **Entity-Relationship Modeling**
4. **Database Design & Normalization**
5. **Implementation Details**
6. **Query Development & Testing**
7. **Results & Performance Metrics**
8. **Conclusion & Future Enhancements**

## 🚀 Getting Started

### Prerequisites
- Microsoft SQL Server (2019 or later)
- SQL Server Management Studio (SSMS)
- Basic understanding of T-SQL

### Installation Steps
1. **Clone the repository**
   ```bash
   git clone https://github.com/Maira-Tanveer/Cinema-Information-Management-System/blob/66d90d880570b4c23235f3dc353ccb79f2fb258d/Cinema%20Information%20Management%20System.pdf
   cd cinema-management-system
   ```

2. **Create Database**
   ```sql
   CREATE DATABASE CinemaManagementDB;
   USE CinemaManagementDB;
   ```

3. **Execute Scripts in Order**
   - Run `01_Table_Creation.sql`
   - Run `02_Data_Insertion.sql`
   - Test with `03_Sample_Queries.sql`

4. **Verify Installation**
   ```sql
   SELECT COUNT(*) FROM Movies;
   SELECT COUNT(*) FROM Customers;
   SELECT COUNT(*) FROM Tickets;
   ```

## 🔍 Query Examples & Use Cases

### 🎬 Business Intelligence Queries

#### Monthly Revenue Analysis
```sql
SELECT 
    MONTH(t.booking_date) as month,
    YEAR(t.booking_date) as year,
    COUNT(t.ticket_id) as total_tickets,
    SUM(t.ticket_price) as ticket_revenue,
    (SELECT SUM(oi.quantity * oi.unit_price) 
     FROM Food_Orders fo 
     JOIN Order_Items oi ON fo.order_id = oi.order_id 
     WHERE MONTH(fo.order_date) = MONTH(t.booking_date)
     AND YEAR(fo.order_date) = YEAR(t.booking_date)) as food_revenue
FROM Tickets t
GROUP BY MONTH(t.booking_date), YEAR(t.booking_date)
ORDER BY year DESC, month DESC;
```

#### Customer Loyalty Analysis
```sql
SELECT 
    c.customer_name,
    c.email,
    COUNT(t.ticket_id) as total_bookings,
    SUM(t.ticket_price) as total_spent,
    AVG(t.ticket_price) as avg_ticket_price
FROM Customers c
JOIN Tickets t ON c.customer_id = t.customer_id
GROUP BY c.customer_id, c.customer_name, c.email
HAVING COUNT(t.ticket_id) >= 5
ORDER BY total_spent DESC;
```

## 🔧 Advanced Features

### 🔐 Security Implementation
- **User Roles**: Admin, Manager, Staff, Customer
- **Data Encryption**: Sensitive customer information
- **Access Control**: Role-based query permissions
- **Audit Trail**: Transaction logging for ticket sales

### 📈 Performance Optimization
- **Indexing Strategy**: Primary and foreign key optimization
- **Query Optimization**: Efficient JOINs and subqueries
- **Data Partitioning**: Large table management
- **Caching**: Frequently accessed movie and showtime data

### 🔄 Future Enhancements
- **Online Booking Portal**: Web interface integration
- **Mobile App API**: RESTful services for mobile applications
- **Analytics Dashboard**: Real-time business intelligence
- **Loyalty Program**: Customer reward point system
- **Multi-Cinema Support**: Chain management capabilities

## 🤝 Contributing

We welcome contributions to enhance this cinema management system! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### 📝 Contribution Areas
- Additional SQL queries for business scenarios
- Performance optimization suggestions
- Database schema enhancements
- Documentation improvements
- Test data generation scripts

## 📞 Contact Information

### 👩‍💻 Team Members
- **Jaweria Fayyaz**
  - Email: jaweria.fayyaz@student.gcu.edu.pk
  - GitHub: [@jaweria-fayyaz](https://github.com/jaweria-fayyaz)

- **Maira Tanveer**
  - Email: maira.tanveer@student.gcu.edu.pk
  - GitHub: [@maira-tanveer](https://github.com/maira-tanveer)

### 🏫 Academic Supervisor
- **Course Instructor**: [sir Nadeem zafar]
- **Department**: Computer Science, GC University Lahore

## 📜 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 🙏 Acknowledgments

- **Cinepax Cinema Chain** for real-world inspiration
- **GC University, Lahore** for academic guidance
- **Microsoft SQL Server** for robust database platform
- **Draw.io** for professional ER diagram creation
- **Database Systems Course** instructors and peers

**⭐ Star this repository if you found it helpful!**

---

*This project demonstrates comprehensive database design principles and real-world application development skills acquired through academic coursework in Database Systems.*
