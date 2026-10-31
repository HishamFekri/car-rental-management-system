# Car Rental System

A desktop app for managing a car rental business: the car inventory, customer records, and renting cars to customers. It is built with Java Swing and stores its data in SQLite.

Built for the Software Construction course, 2023–2024.

### Project Background

This project was developed in 2024 as part of a university Software Construction course. It was a collaborative student project, and the original code was maintained in a teammate's GitHub repository.

This repository is my personal copy of the project, published to document my university work and early experience with Java desktop development.

## Features

- **Accounts.** Sign up and log in. Each account is a username and password stored in the local database.
- **Car management.** Add, update, delete and search cars. Each car has a type, brand, model, manufacture year, color, license plate (format `ABC-123`), hourly rate and availability status.
- **Customer management.** Add, update, delete and search customers by ID, name or email.
- **Renting.** Browse available cars, choose a car and a customer ID, and rent it. The car is then marked `Rented` and linked to that customer.

## Tech stack

| | |
|---|---|
| Language | Java (project targets Java 19, also runs on newer JDKs) |
| UI | Swing, designed with the NetBeans GUI Builder (`.form` files) |
| Database | SQLite, through `sqlite-jdbc-3.20.1.jar` |
| Tables in the UI | `rs2xml.jar` (`DbUtils.resultSetToTableModel`) |
| Build | Apache Ant (NetBeans project) |

## Getting started

### Requirements

- JDK 19 or newer
- [Apache NetBeans](https://netbeans.apache.org/), recommended because the UI layout uses NetBeans' `AbsoluteLayout` library

### Run from NetBeans

1. Clone the repository:
   ```bash
   git clone https://github.com/HishamFekri/car-rental-management-system.git
   ```
2. In NetBeans, open the cloned folder with **File → Open Project**.
3. If NetBeans reports missing references, open **Project Properties → Libraries** and point them to `sqlite-jdbc-3.20.1.jar` and `rs2xml.jar` in the project root.
4. Press **Run** (F6). The main class is `login.LoginTable1`.

### Run the JAR

**Clean and Build** in NetBeans (or `ant jar`) creates `dist/Login.jar`, with its libraries in `dist/lib/`. Run it from the project root so the app can find the database:

```bash
java --enable-native-access=ALL-UNNAMED -jar dist/Login.jar
```

On Java 22 and later, `--enable-native-access` hides a warning from the SQLite driver. On older JDKs you can leave it out.

> `dist/` is in `.gitignore`, so you have to build the JAR before you can run it.

### First login

There is no default account. Click **Sign Up** on the login screen, create a user, then log in with it.

## Database

The app connects to `LoginDataBase.sqlite` with a **relative path** (`jdbc:sqlite:LoginDataBase.sqlite`). That means the working directory must be the project root, or the app won't find the file.

| Table | Purpose |
|---|---|
| `LoginDB` | User accounts (`Username`, `Password`) |
| `Car3` | Cars: ID, type, brand, model, year, color, license plate, availability, hourly rate, `CustomerRenter` |
| `Customer4` | Customers (`ID`, `Name`, `Email`) |

## Project structure

```text
src/login/
├── Login.java                    # Entry point that opens the login window
├── LoginTable1.java              # Login screen (project main class)
├── Registration.java             # Sign-up screen
├── Menu.java                     # Main menu
├── CarInfoManagement.java        # Car list: search and delete
├── AddCar.java / UpdateCar.java
├── CustomersInfoManagament.java  # Customer list: search and delete
├── AddACustomer.java / UpdateCustmoerInfo.java
├── RentCar.java                  # Rent an available car to a customer
└── DBConnection.java             # SQLite connection helper
src/Images/                       # Icons and logo
```

## Known limitations

- Passwords are stored in plain text.
- The database path is relative, so you have to launch the app from the project root.
- There is no "return car" action yet. To return a car, set its availability back to `Available` in **Update Car**.

## Ideas for future work

- Validate input more strictly, for example reject a negative hourly rate.
- Hash passwords before storing them.
- Add a return-car flow and a rental history.
