# MySQL to Oracle SQL Converter

This PHP package provides a utility to convert MySQL SQL queries into Oracle-compatible SQL queries. It handles differences in SQL syntax between MySQL and Oracle, including quoting identifiers, converting functions, and managing specific SQL clauses.

## Installation

To use this package, include the `MySQLToOracleConverter.php` file in your project and ensure you have a PDO connection object ready.

### Requirements

- PHP 7.0 or higher
- PDO extension enabled
- Oracle and MySQL drivers installed

##Methods
1-convertSqlForOracle
-public static function convertSqlForOracle(string &$sql): void
2-execute
-public static function execute(string $sql, ?array $params = null, PDO $connection): PDOStatement
Executes an SQL statement. If the database type is set to 'ORACLE', it first converts the SQL to Oracle-compatible syntax.
$sql: The SQL query to execute.
$params: Optional parameters for the query.
$connection: The PDO connection object.
Returns: The prepared and executed PDO statement.
3-insert
-public static function insert(string $sql, ?array $params = null, PDO $connection): int
Inserts a record into the database and returns the last insert ID.
$sql: The SQL query to execute.
$params: Optional parameters for the query.
$connection: The PDO connection object.
Returns: The last insert ID.
4-removeAliases
public static function removeAliases(string $sql): string
Removes aliases from the SQL query.
$sql: The SQL query to process.
Returns: The SQL query without aliases.
#License
This project is licensed under the MIT License. See the LICENSE file for details.

#Contributing
Feel free to fork this repository and submit pull requests. Any contributions are appreciated!

#Author
Farzan Mohammadi


## Usage

```php
use DatabaseConverter\MySQLToOracleConverter;
use PDO;

// Define your database connection parameters
define('DB_TYPE', 'ORACLE'); // or 'MYSQL'
$dbtns = 'your_tns_string';
$db_username = 'your_username';
$db_password = 'your_password';

$connection = new PDO("oci:dbname=" . $dbtns . ";charset=utf8", $db_username, $db_password, array(
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_EMULATE_PREPARES => false,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_NUM
));

$converter = new MySQLToOracleConverter();

$mysqlQuery = "SELECT * FROM users WHERE id = :id LIMIT 1";
$params = [':id' => 123];

// Convert and execute the query
$stmt = $converter::execute($mysqlQuery, $params, $connection);
$result = $stmt->fetchAll(PDO::FETCH_ASSOC);
