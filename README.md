# ShelfCheck

A JavaFX desktop app for managing library records stored in CSV files. It imports book, student and transaction data, flags invalid records so they can be corrected in place, and provides book search and issue reports.

![Java](https://img.shields.io/badge/Java-25-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![JavaFX](https://img.shields.io/badge/JavaFX-21-1F1F1F?style=flat-square)
![Maven](https://img.shields.io/badge/Maven-build-C71A36?style=flat-square&logo=apachemaven&logoColor=white)
![JUnit](https://img.shields.io/badge/JUnit-tests-25A162?style=flat-square&logo=junit5&logoColor=white)

---

## Features

**Import and error correction**
- Load `book.csv`, `student.csv` and `transaction.csv` from disk
- Every record is validated on import. Valid rows are highlighted green and invalid rows red
- Select any row, edit it in place, and re-validate instantly
- Save the corrected data back out as clean CSV files

**Book search**
- Search by exact title, or use a trailing `*` for prefix matching (e.g. `clean*`)
- Shows total copies, available copies and price for each match
- Export results to a formatted `.txt` report

**Reports**
- Average cost of all valid books in the library
- Books-issued report for any selected date

## Validation Rules

| Field | Rule |
|---|---|
| Student ID | Exactly 8 digits |
| ISBN | ISBN-13 with a `978` or `979` prefix and a valid checksum. Hyphens and spaces are ignored |
| Copies | Between 0 and 2 |
| Availability | Between 0 and the number of copies |
| Date | Real calendar date in `dd/MM/yyyy` format |

## Getting Started

**Requirements:** JDK 25. Maven is not required because the project includes the Maven wrapper.

```bash
git clone https://github.com/Ayura-Divyan/Library-System-Java.git
cd Library-System-Java

# macOS / Linux
./mvnw clean javafx:run

# Windows
mvnw.cmd clean javafx:run
```

Once the app opens, go to **Import Data → Load CSV Files** and select the three files in the `data/` folder, in this order: books, students, transactions.

## Data Format

```text
book.csv         book_id,isbn,title,copies,availability,price
student.csv      student_id,first_name
transaction.csv  transaction_id,date,book_id,student_id,type
```

In `transaction.csv`, `type` is `1` for an issue and `2` for a return.

## Project Structure

```text
src/main/java/com/example/librarysystemjava/
├── Main.java, Launcher.java      App entry point
├── MainController.java           Navigation between screens
├── ImportController.java         Import, highlighting, editing and saving
├── SearchController.java         Title search and export
├── ReportController.java         Average cost and issue reports
├── FileHandler.java              CSV parsing, validation split and saving
├── Validator.java                Field validation rules
├── DataSingleton.java            Shared data across screens
└── Book.java, Student.java, Transaction.java
src/main/resources/.../           FXML layouts for each screen
data/                             Sample CSV files
tests/                            JUnit tests for Validator
```

## Built With

- Java 25 and JavaFX 21 (FXML)
- Maven
- JUnit
