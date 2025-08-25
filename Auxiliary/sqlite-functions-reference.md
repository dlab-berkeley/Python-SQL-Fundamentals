# SQLite Functions Reference Guide

## Aggregate Functions

### COUNT()
Counts the number of rows or non-NULL values.
```sql
SELECT COUNT(*) FROM users;
SELECT COUNT(DISTINCT city) FROM users;
```

### SUM()
Calculates the sum of numeric values.
```sql
SELECT SUM(amount) FROM orders;
SELECT SUM(quantity * price) FROM order_items;
```

### AVG()
Calculates the average of numeric values.
```sql
SELECT AVG(age) FROM users;
SELECT AVG(DISTINCT price) FROM products;
```

### MIN() / MAX()
Returns the minimum or maximum value.
```sql
SELECT MIN(created_date) FROM posts;
SELECT MAX(salary) FROM employees;
```

### GROUP_CONCAT()
Concatenates values from multiple rows into a single string.
```sql
SELECT GROUP_CONCAT(name) FROM users;
SELECT GROUP_CONCAT(name, ', ') FROM users;
SELECT GROUP_CONCAT(DISTINCT category) FROM products;
```

## String Functions

### LENGTH()
Returns the length of a string.
```sql
SELECT LENGTH('Hello World');  -- Returns: 11
SELECT name, LENGTH(name) FROM users;
```

### UPPER() / LOWER()
Converts string to uppercase or lowercase.
```sql
SELECT UPPER('hello');  -- Returns: HELLO
SELECT LOWER('WORLD');  -- Returns: world
```

### SUBSTR()
Extracts a substring from a string.
```sql
SELECT SUBSTR('Hello World', 1, 5);  -- Returns: Hello
SELECT SUBSTR('Hello World', 7);     -- Returns: World
SELECT SUBSTR(email, 1, INSTR(email, '@') - 1) FROM users;  -- Get username from email
```

### REPLACE()
Replaces occurrences of a substring.
```sql
SELECT REPLACE('Hello World', 'World', 'SQLite');  -- Returns: Hello SQLite
UPDATE users SET phone = REPLACE(phone, '-', '');
```

### TRIM() / LTRIM() / RTRIM()
Removes whitespace from strings.
```sql
SELECT TRIM('  Hello  ');    -- Returns: 'Hello'
SELECT LTRIM('  Hello  ');   -- Returns: 'Hello  '
SELECT RTRIM('  Hello  ');   -- Returns: '  Hello'
SELECT TRIM('***Hello***', '*');  -- Returns: 'Hello'
```

### INSTR()
Returns the position of a substring.
```sql
SELECT INSTR('Hello World', 'World');  -- Returns: 7
SELECT INSTR('Hello', 'xyz');          -- Returns: 0
```

### PRINTF()
Formats strings (similar to C printf).
```sql
SELECT PRINTF('%.2f', 123.456);        -- Returns: 123.46
SELECT PRINTF('%04d', 42);             -- Returns: 0042
SELECT PRINTF('%s is %d years old', name, age) FROM users;
```

### || (Concatenation Operator)
Concatenates strings.
```sql
SELECT first_name || ' ' || last_name AS full_name FROM users;
SELECT 'Order #' || order_id FROM orders;
```

## Date and Time Functions

### DATE()
Extracts the date part.
```sql
SELECT DATE('2024-03-15 10:30:45');  -- Returns: 2024-03-15
SELECT DATE('now');                   -- Current date
SELECT DATE('now', '+1 day');        -- Tomorrow
```

### TIME()
Extracts the time part.
```sql
SELECT TIME('2024-03-15 10:30:45');  -- Returns: 10:30:45
SELECT TIME('now');                   -- Current time
```

### DATETIME()
Returns a datetime string.
```sql
SELECT DATETIME('now');                        -- Current datetime
SELECT DATETIME('now', '+1 hour');            -- One hour from now
SELECT DATETIME('now', '-30 minutes');        -- 30 minutes ago
SELECT DATETIME('now', 'start of month');     -- First day of current month
```

### STRFTIME()
Formats date/time values.
```sql
SELECT STRFTIME('%Y-%m-%d', 'now');           -- 2024-03-15
SELECT STRFTIME('%H:%M', 'now');              -- 14:30
SELECT STRFTIME('%w', 'now');                 -- Day of week (0-6)
SELECT STRFTIME('%Y', 'now') - STRFTIME('%Y', birth_date) AS age FROM users;
```

### JULIANDAY()
Converts to Julian day number (useful for date calculations).
```sql
SELECT JULIANDAY('now') - JULIANDAY(created_date) AS days_ago FROM posts;
SELECT JULIANDAY('2024-12-31') - JULIANDAY('2024-01-01');  -- Days in year
```

### Date Modifiers
Common modifiers for date functions:
```sql
-- Relative modifiers
'+N days', '-N days'
'+N months', '-N months'
'+N years', '-N years'
'+N hours', '-N hours'
'+N minutes', '-N minutes'
'+N seconds', '-N seconds'

-- Absolute modifiers
'start of month'
'start of year'
'start of day'
'weekday N'  -- Next weekday N (0=Sunday)
```

## Mathematical Functions

### ABS()
Returns absolute value.
```sql
SELECT ABS(-42);     -- Returns: 42
SELECT ABS(10 - 20); -- Returns: 10
```

### ROUND()
Rounds a number.
```sql
SELECT ROUND(3.14159);        -- Returns: 3.0
SELECT ROUND(3.14159, 2);     -- Returns: 3.14
SELECT ROUND(123.456, -1);    -- Returns: 120.0
```

### CEIL() / FLOOR()
Ceiling and floor functions.
```sql
SELECT CEIL(4.2);   -- Returns: 5
SELECT FLOOR(4.8);  -- Returns: 4
```

### RANDOM()
Generates random numbers.
```sql
SELECT RANDOM();                           -- Random integer
SELECT ABS(RANDOM()) % 100;              -- Random 0-99
SELECT * FROM users ORDER BY RANDOM() LIMIT 5;  -- Random 5 users
```

### MIN() / MAX() (Scalar)
Returns minimum or maximum of values.
```sql
SELECT MIN(10, 20, 5);   -- Returns: 5
SELECT MAX(10, 20, 5);   -- Returns: 20
```

### POWER() / SQRT()
Power and square root functions.
```sql
SELECT POWER(2, 10);    -- Returns: 1024
SELECT SQRT(16);        -- Returns: 4
```