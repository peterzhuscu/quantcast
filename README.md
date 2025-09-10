# 🍪 Most Active Cookie Finder

A Java application that finds the most active cookie from a log file for a given date.

## 📂 Project Structure

```
most-active-cookie/
├── pom.xml
├── cookie_log.csv
├── cookie-finder          # Linux/macOS wrapper script
├── cookie-finder.bat      # Windows wrapper script
└── src/
    ├── main/
    │   └── java/
    │       └── CookieFinder.java
    └── test/
        └── java/
            └── CookieFinderTest.java
```

---

## ⚙️ Requirements

* Java 8+
* Maven 3+

---

## 🚀 Build & Run

### 1. Build the project

```bash
mvn clean package
```

This creates an executable JAR at: `target/most-active-cookie-1.0-SNAPSHOT.jar`

### 2. Run with JAR

```bash
java -jar target/most-active-cookie-1.0-SNAPSHOT.jar -f cookie_log.csv -d 2018-12-09
```

**Output:**
```
AtY0laUfhglK3lC7
```

### 3. Run with wrapper scripts

**Linux/macOS:**
```bash
chmod +x cookie-finder
./cookie-finder -f cookie_log.csv -d 2018-12-09
```

**Windows:**
```cmd
cookie-finder.bat -f cookie_log.csv -d 2018-12-09
```

---

## 📋 Usage Options

| Option | Description | Required |
|--------|-------------|----------|
| `-f` | Path to CSV log file | Yes |
| `-d` | Date (YYYY-MM-DD format) | Yes |
| `--help` | Show help message | No |

**Examples:**
```bash
# Basic usage
./cookie-finder -f cookie_log.csv -d 2018-12-09

# Different file
./cookie-finder -f /path/to/logs.csv -d 2018-12-08

# Show help
./cookie-finder --help
```

---

## 🧪 Testing

Run tests:
```bash
mvn test
```

Test cases cover:
* Single most active cookie
* Multiple cookies with same count
* No cookies for given date
* Invalid file formats
* Edge cases

---

## 📄 Log File Format

CSV format with two columns:

```csv
cookie,timestamp
cookie_id,YYYY-MM-DDThh:mm:ss+00:00
```

**Sample file (`cookie_log.csv`):**
```csv
cookie,timestamp
AtY0laUfhglK3lC7,2018-12-09T14:19:00+00:00
SAZuXPGUrfbcn5UA,2018-12-09T10:13:00+00:00
5UAVanZf6UtGyKVS,2018-12-09T07:25:00+00:00
AtY0laUfhglK3lC7,2018-12-09T06:19:00+00:00
SAZuXPGUrfbcn5UA,2018-12-09T22:03:00+00:00
AtY0laUfhglK3lC7,2018-12-08T14:19:00+00:00
```

**Important notes:**
- Headers are required
- Timestamps must be in ISO format with timezone
- File must be valid CSV format

---

## 🔍 How It Works

1. **Parse** the CSV file line by line
2. **Filter** entries matching the target date
3. **Count** occurrences of each cookie
4. **Find** cookie(s) with the highest count
5. **Output** result(s) (one per line if multiple)

**Example with tied cookies:**
```
AtY0laUfhglK3lC7
SAZuXPGUrfbcn5UA
```

---

## 🚨 Error Handling

Common errors and solutions:

| Error | Cause | Solution |
|-------|--------|----------|
| File not found | Wrong file path | Check file path exists |
| Invalid date | Wrong date format | Use YYYY-MM-DD format |
| Parse error | Malformed CSV | Verify CSV structure |
| No results | No data for date | Check date and file content |

---

## 📝 Development

**Build without tests:**
```bash
mvn clean package -DskipTests
```

**Clean build:**
```bash
mvn clean compile
```

**Run specific test:**
```bash
mvn test -Dtest=CookieFinderTest
```