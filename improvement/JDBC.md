# JDBC API в Java: Структурований Огляд

---

## 1. Визначення та Призначення
**Java Database Connectivity (JDBC)** — це **API** для мови Java, що визначає, як клієнт може отримати доступ до бази даних.

- **Призначення:** Стандартизований спосіб взаємодії Java-додатків з реляційними базами даних.
- **Платформа:** Частина **Java SE** від Oracle Corporation.
- **Офіційна документація:** [Oracle JDBC Overview](https://docs.oracle.com/en/database/oracle/oracle-database/26/jjdbc/overview-Oracle-JDBC.html)

---

## 2. Основні Сутності (Інтерфейси)
JDBC API складається з ключових інтерфейсів:

- `Connection`: З'єднання з базою даних.
- `Statement`, `PreparedStatement`, `CallableStatement`: Виконання SQL-запитів.
- `ResultSet`: Обробка результатів запитів.
- `Driver`: Реєстрація драйвера.

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

> З Java 6+ драйвери JDBC, що підтримують SPI, реєструються автоматично при наявності в classpath. Виклик `Class.forName(...)` потрібен лише для старих драйверів або специфічних сценаріїв.

- `DatabaseMetaData`: Метадані бази даних.

---

## 3. Типи Statement та їх Використання

| Тип | Призначення | Особливості |
| :--- | :--- | :--- |
| `Statement` | Загальні SQL-запити | Виконується кожного разу без кешування |
| `PreparedStatement` | Запити з параметрами (`?`) | Кешується та компілюється на сервері |
| `CallableStatement` | Виклик збережених процедур | Працює з `stored procedures` |

---

## 4. Переваги PreparedStatement

**Рекомендується використовувати `PreparedStatement` для:**

1. **Безпеки:** Захист від SQL-ін'єкцій.
2. **Продуктивності:** Кешування запитів на сервері.
3. **Перевикористання:** Ефективне повторне використання запитів.
4. **Зручності:** Динамічні параметризовані запити.

---

## 5. Транзакції (Commit & Rollback)

| Операція | Метод |
| :--- | :--- |
| Вимкнути auto-commit | `conn.setAutoCommit(false);` |
| Фіксація | `conn.commit();` |
| Відкат | `conn.rollback();` |

---

## 6. Класифікація JDBC-драйверів

| Тип | Опис | Статус |
| :--- | :--- | :--- |
| Type 1 | JDBC-ODBC Bridge | Застарів |
| Type 2 | Native API | Залежить від клієнтської платформи |
| Type 3 | Network Protocol | Java-драйвер + проміжний сервер |
| Type 4 | Pure Java | Найпоширеніший, напряму з БД |

### Приклади

- **Type 1:**
  ```java
  Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");
  Connection conn = DriverManager.getConnection("jdbc:odbc:myDSN");
  ```

- **Type 2:**
  ```java
  Class.forName("oracle.jdbc.OracleDriver");
  Connection conn = DriverManager.getConnection("jdbc:oracle:oci:@mydb", "user", "pass");
  ```

- **Type 3:**
  ```java
  Class.forName("com.ddtek.jdbc.sqlserver.SQLServerDriver");
  Connection conn = DriverManager.getConnection("jdbc:datadirect:sqlserver://host:port;DatabaseName=db", "user", "pass");
  ```

- **Type 4:**
  ```java
  Class.forName("com.mysql.cj.jdbc.Driver");
  Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "pass");
  ```

---

## 7. Рівні Ізоляції Транзакцій

| Рівень | Dirty Reads | Non-Repeatable Reads | Phantom Reads |
| :--- | :--- | :--- | :--- |
| `READ_UNCOMMITTED` | ✅ | ✅ | ✅ |
| `READ_COMMITTED` | ❌ | ✅ | ✅ |
| `REPEATABLE_READ` | ❌ | ❌ | ✅ |
| `SERIALIZABLE` | ❌ | ❌ | ❌ |

---

## 8. Savepoint

```java
Savepoint sp = conn.setSavepoint("Step1");
conn.rollback(sp);
conn.commit(); // завершення після часткового відкату
```

---

## 9. Керування Ресурсами та Створення З'єднання

### Закриття ресурсів

```java
try (Connection conn = DriverManager.getConnection(
    "jdbc:vendor:connectionDetails",
    "username",
    "password")) {
    // Використання з'єднання
}
```

### Альтернатива: DataSource

```java
DataSource ds = new MysqlDataSource();
ds.setURL("jdbc:mysql://localhost:3306/mydb");
ds.setUser("username");
ds.setPassword("password");

try (Connection conn = ds.getConnection()) {
    // Використання з'єднання
}
```

---

## 10. Метадані Бази Даних та Результатів

| Інтерфейс | Призначення | Отримання |
| :--- | :--- | :--- |
| `DatabaseMetaData` | Інформація про БД | `conn.getMetaData()` |
| `ResultSetMetaData` | Інформація про результат запиту | `rs.getMetaData()` |

### Приклади

- **DatabaseMetaData:**
  ```java
  DatabaseMetaData meta = conn.getMetaData();
  System.out.println(meta.getDatabaseProductName());
  System.out.println(meta.getDriverVersion());
  ```

- **ResultSetMetaData:**
  ```java
  ResultSet rs = stmt.executeQuery("SELECT * FROM users");
  ResultSetMetaData rsMeta = rs.getMetaData();
  System.out.println(rsMeta.getColumnCount());
  System.out.println(rsMeta.getColumnName(1));
  ```

---

## 11. Додаткові Ресурси

- [Oracle JDBC Overview](https://docs.oracle.com/en/database/oracle/oracle-database/26/jjdbc/overview-Oracle-JDBC.html)
- [TutorialsPoint JDBC](https://www.tutorialspoint.com/jdbc/index.htm)
- [Jenkov JDBC Tutorial](http://tutorials.jenkov.com/jdbc/index.html)
- [Proselyte JDBC Guide](http://proselyte.net/tutorials/jdbc/)
- [Baeldung JDBC Guide](https://www.baeldung.com/java-jdbc)
- [Spring JDBC Docs](https://docs.spring.io/spring-framework/reference/data-access/jdbc.html)

---

## Apendix: RowSet, BatchUpdate, Connection Pooling

### RowSet

```java
RowSetFactory factory = RowSetProvider.newFactory();
CachedRowSet rowSet = factory.createCachedRowSet();
rowSet.setUrl("jdbc:mysql://localhost:3306/mydb");
rowSet.setUsername("user");
rowSet.setPassword("pass");
rowSet.setCommand("SELECT * FROM users");
rowSet.execute();
```

### BatchUpdate

```java
PreparedStatement ps = conn.prepareStatement("INSERT INTO users(name) VALUES(?)");
for (String name : names) {
    ps.setString(1, name);
    ps.addBatch();
}
int[] results = ps.executeBatch();
System.out.println("Inserted rows: " + results.length);
```

### Connection Pooling

```java
HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/mydb");
config.setUsername("user");
config.setPassword("pass");

HikariDataSource ds = new HikariDataSource(config);
try (Connection conn = ds.getConnection()) {
    // Використання з’єднання
}
```

---

## Apendix: Spring JDBC / JdbcTemplate

```java
JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
List<User> users = jdbcTemplate.query(
    "SELECT * FROM users",
    new BeanPropertyRowMapper<>(User.class)
);
```

---

## Apendix: R2DBC — реактивна альтернатива JDBC

> **R2DBC (Reactive Relational Database Connectivity)** — це **окремий драйвер**, який **не базується на JDBC API**. Він створений для реактивного доступу до реляційних баз даних, працює з Project Reactor і підтримується Spring WebFlux.

```java
Mono<Connection> connection = connectionFactory.create();
connection.flatMapMany(conn ->
    conn.createStatement("SELECT * FROM users").execute()
);
```

(Додано Copilot) R2DBC — неблокуюча альтернатива JDBC, актуальна для високонавантажених реактивних застосунків у 2025 році. Він не використовує `DriverManager` і не реалізує JDBC-інтерфейси — це окрема екосистема з власними драйверами (наприклад, `r2dbc-postgresql`, `r2dbc-mysql`).


---

## Apendix: UML-схема (текстова)

```
DriverManager
    ↓
Connection
    ↓
Statement / PreparedStatement / CallableStatement
    ↓
ResultSet
```

---

## Apendix: CRUD з PreparedStatement

```java
// INSERT
PreparedStatement insert = conn.prepareStatement("INSERT INTO users(name) VALUES(?)");
insert.setString(1, "Alice");
insert.executeUpdate();

// SELECT
PreparedStatement select = conn.prepareStatement("SELECT * FROM users WHERE name = ?");
select.setString(1, "Alice");
ResultSet rs = select.executeQuery();
while (rs.next()) {
    System.out.println(rs.getString("name"));
}

// UPDATE
PreparedStatement update = conn.prepareStatement("UPDATE users SET name = ? WHERE id = ?");
update.setString(1, "Bob");
update.setInt(2, 1);
update.executeUpdate();

// DELETE
PreparedStatement delete = conn.prepareStatement("DELETE FROM users WHERE id = ?");
delete.setInt(1, 1);
delete.executeUpdate();
```

(Додано Copilot) Цей приклад охоплює базові CRUD-операції з параметризованими запитами — рекомендований підхід для безпечної та контрольованої роботи з базою даних.
