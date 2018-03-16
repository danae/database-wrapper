**database-wrapper** is a easy-to-use PDO wrapper for PHP 7.0 or higher.

## Installation

database-wrapper is best installed using Composer. The library is found as `dengsn/database-wrapper` in the Packagist repository. If your project does not use composer, you can download the latest release or the dev-master branch as an archive.

## Usage

### Creating a new instance

```php
$db = new Database\Database(string $dsn, string $username = '', string $password = '', array $options = []);
```

The arguments of the constructor are the same as when creating a new PDO object. The `$username`, `$password` and `$options` arguments default to an empty string or array if they're not given.

Furthermore you can use every function of the PDO class directly on the Database class because of an internal __call function that forwards unknown function calls to the underlying PDO object.

### Select queries
```php
$db->select(string $table, array $where = [], string $order = '');
$db->selectOne(string $table, array $where = [], string $order = '');
```

The **select** and **selectOne** functions perform a "SELECT" query to the table provided by the `$table` argument.

#### Arguments
* `$table`: the table to select from.
* `$where`: an associative array consisting of key-value pairs that are treated as "WHERE" clause. The pairs are merged using "OR" operators or "LIKE" clauses.
* `$order`: specifies a string that is appended as an "ORDER BY" argument.

#### Return value
**select** returns an array of matched rows in the table while **selectOne** returns only the first row (thr result of "LIMIT 1"). The rows are associative arrays with keys that match the column name.

### Insert, update and delete queries
```php
$db->insert(string $table, array $object);
$db->update(string $table, array $object, array $where);
$db->delete(string $table, array $where);
```

The **insert**, **update** and **delete** functions perform "INSERT", "UPDATE" and "DELETE" queries respectively.

#### Arguments
* `$table`: the table to perform the query on.
* `$object`: an array of key-value pairs that represent the row to insert/update. The keys of the array represent the column names.
* `$where`: an associative array consisting of key-value pairs that are treated as "WHERE" clause.

#### Return value
All three functions return the number of rows that were affected by the query.
