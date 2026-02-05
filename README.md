# Finance Tracker

A comprehensive personal finance management application built with Java Swing that helps users track their income, expenses, and generate financial reports. This project was developed as part of an Object-Oriented Programming II group assignment.

## 📋 Features

- **User Authentication**: Secure registration and login system with encrypted password storage
- **Income Management**: Track multiple income sources with categories, amounts, dates, and notes
- **Expense Tracking**: Monitor expenses across different categories with detailed information
- **Real-time Balance**: View current balance based on total income and expenses
- **Visual Reports**: Generate pie charts and visual reports to analyze spending patterns
- **Category Management**: Add custom categories for both income and expenses
- **Multi-threaded Operations**: Efficient background processing using Java threads
- **Data Persistence**: MySQL database integration for secure data storage
- **User-friendly GUI**: Intuitive interface built with Java Swing components

## 🛠️ Technology Stack

- **Language**: Java
- **GUI Framework**: Java Swing
- **Database**: MySQL
- **Libraries**:
  - JFreeChart 1.0.19 (for chart generation)
  - JCalendar 1.4 (for date selection)
  - Apache POI 5.2.2 (for report generation)
  - Apache Log4j 2.17.1 (for logging)
  - MySQL Connector/J (JDBC driver)
  - AbsoluteLayout

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Java Development Kit (JDK)** 8 or higher
- **MySQL Server** 5.7 or higher
- **NetBeans IDE** (recommended, as the project is configured for NetBeans)
- **MySQL Workbench** (optional, for database management)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/janithjay/-Finance-Tracker.git
cd -Finance-Tracker
```

### 2. Database Setup

Run the provided SQL script to create the database and tables:

```bash
mysql -u root -p < "finance tracker.sql"
```

Or manually execute the SQL file in MySQL:

1. Open MySQL Workbench or command line
2. Run the following commands:

```sql
CREATE DATABASE finance_tracker;
USE finance_tracker;

-- Create user_table
CREATE TABLE user_table (
    user_name CHAR(50) NOT NULL PRIMARY KEY,
    email CHAR(50) NOT NULL,
    passwd CHAR(50) NOT NULL
);

-- Create incomes table
CREATE TABLE incomes (
    income_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    user_name CHAR(50) NOT NULL,
    amount FLOAT(15, 2) NOT NULL CHECK (amount > 0),
    category CHAR(50) NOT NULL,
    `date` DATE,
    notes VARCHAR(255),
    CONSTRAINT fk1 FOREIGN KEY (user_name) REFERENCES user_table(user_name)
);

-- Create expenses table
CREATE TABLE expenses (
    expenses_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    user_name CHAR(50) NOT NULL,
    amount FLOAT(15, 2) NOT NULL CHECK (amount > 0),
    category CHAR(50) NOT NULL,
    `date` DATE,
    notes VARCHAR(255),
    CONSTRAINT fk2 FOREIGN KEY (user_name) REFERENCES user_table(user_name)
);
```

### 3. Configure Database Connection

Update the database connection settings in the `DBconnection.java` file:

1. Navigate to: `group assignment/src/group/assignment/DBconnection.java`
2. Update the following constants with your MySQL credentials:

```java
private static final String JDBC_URL = "jdbc:mysql://localhost:3306/finance_tracker?zeroDateTimeBehavior=CONVERT_TO_NULL";
private static final String USERNAME = "your_mysql_username";
private static final String PASSWORD = "your_mysql_password";
```

### 4. Add Required JAR Files

The project requires several external libraries. Make sure all JAR files in the `jar files` directory are properly added to your project's classpath:

- `AbsoluteLayout-RELEASE210.jar`
- `jcalendar-1.4.jar`
- `jcommon-1.0.23.jar`
- `jfreechart-1.0.19.jar`
- Apache Log4j 2.17.1 JARs
- Apache POI 5.2.2 JARs

**In NetBeans:**
1. Right-click on the project → Properties
2. Select "Libraries" → "Compile" tab
3. Click "Add JAR/Folder" and add all required JARs

### 5. Build and Run

**Using NetBeans:**
1. Open the project in NetBeans (`group assignment`)
2. Clean and Build the project (Shift + F11)
3. Run the project (F6)

**Using Command Line:**
```bash
cd "group assignment"
ant clean
ant build
ant run
```

## 💡 Usage

### Getting Started

1. **Registration**: 
   - Launch the application
   - Click on "Register" to create a new account
   - Enter your username, email, and password
   - Click "Submit" to create your account

2. **Login**:
   - Enter your registered username and password
   - Click "Login" to access your finance tracker

3. **Add Income**:
   - Click on the "Income" button
   - Enter amount, select category, choose date, and add notes
   - Click "Add" to save the income entry

4. **Add Expenses**:
   - Click on the "Expenses" button
   - Enter amount, select category, choose date, and add notes
   - Click "Add" to save the expense entry

5. **View Reports**:
   - Click on the "Reports" button
   - View visual representations of your financial data
   - Analyze spending patterns with pie charts

6. **Check Balance**:
   - Your current balance is displayed on the main tracker screen
   - Balance = Total Income - Total Expenses

## 📁 Project Structure

```
-Finance-Tracker/
├── group assignment/
│   ├── src/
│   │   ├── group/
│   │   │   └── assignment/
│   │   │       ├── tracker.java          # Main dashboard
│   │   │       ├── login.java            # Login screen
│   │   │       ├── registration.java     # Registration screen
│   │   │       ├── Income.java           # Income management
│   │   │       ├── Expenses.java         # Expense management
│   │   │       ├── Reports.java          # Report generation
│   │   │       ├── DBconnection.java     # Database connection
│   │   │       ├── Encryption.java       # Password encryption
│   │   │       └── UserThread.java       # Threading support
│   │   └── pics/                         # UI images
│   ├── build/                            # Compiled classes
│   ├── nbproject/                        # NetBeans project files
│   ├── build.xml                         # Ant build script
│   └── manifest.mf                       # JAR manifest
├── jar files/                            # External libraries
├── finance tracker.sql                   # Database schema
├── LICENSE                               # License file
├── .gitignore                           # Git ignore rules
└── README.md                            # This file
```

## 🔒 Security Features

- **Password Encryption**: User passwords are encrypted before storage
- **SQL Injection Prevention**: Prepared statements used for all database queries
- **Input Validation**: Form inputs are validated before processing
- **Secure Authentication**: Login credentials verified against encrypted database entries

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- Group Assignment Project - OOP II Course

## 🐛 Known Issues

- Database credentials are hardcoded (should use configuration files)
- Limited error handling in some UI components
- Chart functionality may require additional configuration

## 🔮 Future Enhancements

- [ ] Add budget planning features
- [ ] Implement recurring transactions
- [ ] Add data export functionality (CSV, PDF)
- [ ] Create mobile-responsive version
- [ ] Add multi-currency support
- [ ] Implement financial goal tracking
- [ ] Add notification system for bill reminders
- [ ] Create detailed analytics dashboard

## 📞 Support

For issues, questions, or contributions, please open an issue in the GitHub repository.

---

**Note**: Remember to update your database credentials in `DBconnection.java` before running the application.
