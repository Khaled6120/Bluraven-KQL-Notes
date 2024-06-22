# Bluraven-KQL-Notes
<br> 

## String Operators

| Operator                | Description                                                                           | Examples                                              |
|-------------------------|---------------------------------------------------------------------------------------|-------------------------------------------------------|
| `==`                    | Case-sensitive equals                                                                 | `FileName == "ntdsutil.exe"`                          |
| `=~`                    | Case-insensitive equals                                                               | `FileName =~ "ntdsutil.exe"`                          |
| `!=`                    | Case-sensitive not equals                                                             | `FileName != "ntdsutil.exe"`                          |
| `!~`                    | Case-insensitive not equals                                                           | `FileName !~ "ntdsutil.exe"`                          |
| `has`                   | Case-insensitive includes whole word                                                  | `FileName has "ntdsutil"`                             |
| `has_cs`                | Case-sensitive includes whole word                                                    | `FileName has_cs "ntdsutil"`                          |
| `!has`                  | Case-insensitive does not include whole word                                          | `FileName !has "setup"`                               |
| `!has_cs`               | Case-sensitive does not include whole word                                            | `FileName !has_cs "setup"`                            |
| `hassuffix`             | Case-insensitive ends with                                                            | `FileName hassuffix "util"`                           |
| `hassuffix_cs`          | Case-sensitive ends with                                                              | `FileName hassuffix_cs "util"`                        |
| `!hassuffix`            | Case-insensitive does not end with                                                    | `FileName !hassuffix "util"`                          |
| `!hassuffix_cs`         | Case-sensitive does not end with                                                      | `FileName !hassuffix_cs "util"`                       |
| `hasprefix`             | Case-insensitive starts with                                                          | `FileName hasprefix "ntds"`                           |
| `hasprefix_cs`          | Case-sensitive starts with                                                            | `FileName hasprefix_cs "ntds"`                        |
| `!hasprefix`            | Case-insensitive does not start with                                                  | `FileName !hasprefix "ntds"`                          |
| `!hasprefix_cs`         | Case-sensitive does not start with                                                    | `FileName !hasprefix_cs "ntds"`                       |
| `has_all`               | Case-insensitive includes all specified values (works like `has` operator)            | `FolderPath has_all ("ntds", "util", "temp")`         |
| `has_any`               | Case-insensitive includes any of the specified values (works like `has` operator)     | `FolderPath has_any ("temp", "tmp", "public")`        |
| `in`                    | Case-sensitive equals to any of the specified values                                   | `FileName in ("rundll32", "dllhost", "powershell")`   |
| `in~`                   | Case-insensitive equals to any of the specified values                                 | `FileName in~ ("rundll32", "dllhost", "powershell")`  |
| `!in`                   | Case-sensitive does not equal to any of the specified values                           | `FileName !in ("svchost", "winlogon")`                |
| `!in~`                  | Case-insensitive does not equal to any of the specified values                         | `FileName !in~ ("svchost", "winlogon")`               |
| `contains`              | Case-insensitive substring appears anywhere                                           | `FileName contains "imikat"`                          |
| `contains_cs`           | Case-sensitive substring appears anywhere                                             | `FileName contains_cs "imikat"`                       |
| `startswith`            | Case-insensitive starts with                                                          | `FileName startswith "mimi"`                          |
| `startswith_cs`         | Case-sensitive starts with                                                            | `FileName startswith_cs "mimi"`                       |
| `endswith`              | Case-insensitive ends with                                                            | `FileName endswith "katz"`                            |
| `endswith_cs`           | Case-sensitive ends with                                                              | `FileName endswith_cs "dogz"`                         |
| `matches regex`         | Case-sensitive regex match                                                            | `FolderPath matches regex ".*TEMP.*"`                 |
| `matches regex (?i)`    | Case-insensitive regex match                                                          | `FolderPath matches regex "(?i).*temp.*"`             |

<br> <br>

## Data Types

| Data Type  | Description                                                                                                         | Example                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| `datetime` | Represents date and time values, always in UTC. Commonly used in queries for specific points in time.               | ``` datetime("2023-10-14 18:15") ```                                                                        |
| `timespan` | Represents durations or lengths of time. Useful for calculating differences between datetime values.                | ``` 1d ``` (1 day), ``` 12h ``` (12 hours)                                                                 |
| `string`   | Represents a sequence of characters. Used for text-based data like computer names, URLs, IP addresses.              | ``` "C:\\Program Files\\Edge\\msedge.exe" ``` or ``` @"C:\Program Files\Edge\msedge.exe" ```               |
| `dynamic`  | A versatile type that can hold any kind of data, including objects and arrays. Useful for JSON-like data structures. | ``` {"HostName":"workstation.domain.local", "IPAddress":"192.168.0.1"} ```                                  |
| `int`      | Represents whole numbers. Commonly used for counting and arithmetic operations.                                     | ``` 42 ```                                                                                                  |
| `long`     | Similar to int but for larger whole numbers. Ideal for large datasets or significant numerical values.              | ``` 123456789012345 ```                                                                                    |
| `real`     | Represents floating-point numbers. Used for precise mathematical computations or managing numbers with decimals.    | ``` 3.14 ```                                                                                                |
| `bool`     | Represents a boolean value, true or false. Used in conditional evaluations.                                         | ``` true ``` or ``` false ```          

<br> <br>

## General Operators
| KQL Operator   | Description                                                                                       | Example                                                                                          |
|----------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| `let`          | Defines a named expression that can be used in subsequent parts of the query, similar to a variable in programming languages. Enhances readability and reusability of common expressions. Must end with a semicolon (`;`). | ``` let user_name = "svc-mssql";<br>let created_services = <br>  DeviceEvents<br>  \| where ActionType == "ServiceInstalled"; ``` |
| `set`          | Modifies the value of a query option for the duration of the query. Useful for adjusting specific options like memory limits temporarily during query execution. Must end with a semicolon (`;`). | ``` set maxmemoryconsumptionperiterator = 9723456780; ```                                        |
| `count`        | Returns the total number of records in a tabular expression. Useful for understanding the volume of data.| ``` DeviceEvents \| count ```                                                                    |
| `take`         | Returns a specified number of rows from a table, but the rows returned are not guaranteed to be random.  | ``` DeviceEvents \| take 10 ```                                                                  |
| `limit`        | Synonym for the `take` operator.                                                                        | ``` DeviceEvents \| limit 10 ```                                                                 |
| `sample`       | Returns a specified number of random rows from a table. Each execution returns different results.       | ``` DeviceEvents \| sample 10 ```                                                                |
| `distinct`     | Returns distinct values of a column or combination of columns. Useful for understanding unique data.    | ``` DeviceEvents \| distinct ActionType ``` <br> ``` DeviceEvents \| distinct ActionType, DeviceName ``` |
| `project`         | Transforms the result set by selecting specific columns, renaming them, creating computed columns, or changing their order. Helps in shaping the output to include only the relevant data.      | ``` T \| project NewColumnName1 = ExistingColumnName1, NewColumnName2 = ExistingColumnName2 + 10 ``` |
| `project-rename`  | Renames columns in the result set without affecting their order or excluding any columns.                       | ``` T \| project-rename NewColumnName1 = ExistingColumnName1, NewColumnName2 = ExistingColumnName2 ``` |
| `project-reorder` | Changes the order of columns in the result set, bringing important columns to the front.                        | ``` T \| project-reorder ExistingColumnName2, ExistingColumnName1 ```                              |
| `project-away`    | Excludes specific columns from the result set, useful when you want to remove a few columns from a large number of them.                                                                                      | ``` T \| project-away UnwantedColumnName1, UnwantedColumnName2 ```                                 |
| `search`        | Searches for text patterns in tables or columns.                              | `search "mimikatz"`                                                           |
| `has`           | Case-insensitive check if a text includes a complete word or term.            | `DeviceEvents \| where FileName has "mimikatz"`                               |
| `hassuffix`     | Case-insensitive check if a text ends with the specified suffix.              | `DeviceEvents \| where FilePath hassuffix "temp"`                             |
| `hasprefix`     | Case-insensitive check if a text starts with the specified prefix.            | `DeviceEvents \| where FilePath hasprefix "C:\Windows"`                       |
| `contains`      | Case-insensitive check if a substring appears anywhere within a text.         | `DeviceEvents \| where FileName contains "mimik"`                             |
| `matches regex` | Uses regular expressions for string matching (case-sensitive).                | `DeviceEvents \| where FileName matches regex @"^mimikatz.*\.dll$"`           |
| `search in`     | Searches within specified tables or columns.                                  | `search in (DeviceProcessEvents) "mimikatz"`                                  |
| `search column` | Searches within a specific column.                                            | `search FileName:"lsass"`                                                     |
| `Where` | Enables precise data filtering based on specified criteria.                                           | `SecurityEvent \ where TimeGenerated > ago(1d) and EventID == 4625 and TargetUserName == "suspicious_user"`                                                     |
| `now()`        | Returns the current date and time at query execution. Can include an optional timespan offset to adjust the returned datetime. | ```SecurityEvent \| where TimeGenerated > now(-1h)``` |
| `ago() `       | Returns a datetime relative to the current moment in the past. Takes a single timespan value as an argument. | ```SecurityEvent \| where TimeGenerated > ago(1h)``` |
| `union `       | Merges the results of two or more tables (or tabular expressions) into a single result set. Optional parameters can modify its behavior. | ```union UserLoginEvents, UserProfiles``` |
| `join  `       | Merges rows from two tables based on matching values in specified columns (keys). Supports various join types (inner, leftouter, etc.). | ```UserLoginEvents \| join kind=inner UserProfiles on UserId``` |
| `summarize  `  | Aggregates data based on specified aggregation functions and grouping columns, converting large datasets into concise insights. | ```SecurityEvent \| summarize Count = count(), AvgCpuUsage = avg(CpuUsage) by Computer``` |

<br> <br>
## Statistical Aggregation
| KQL Function | Description | Syntax | Example Query |
|--------------|-------------|--------|---------------|
| `count() `     | Counts the number of rows in the result set or group. Useful for anomaly detection using static thresholds. | `summarize count()` | ```SecurityEvent \| where EventID == 4624 \| summarize count()``` |
|` dcount() `    | Estimates the number of distinct (unique) values of an expression per group. It's resource-intensive but provides an approximate count with low error probability. | `summarize dcount(<Expression>, <Accuracy>)` | ```DeviceLogonEvents \| where Timestamp > ago(48h) \| where ActionType == "LogonSuccess" \| summarize unique_computer_count = dcount(DeviceName) by AccountName \| where unique_computer_count > 3``` |
| count_distinct() | Counts the number of distinct (unique) values of an expression per group. Offers accurate results but may be slower for large datasets compared to dcount(). | `summarize count_distinct(<Expression>)` | ```SecurityEvent \| where EventID == 4624 \| summarize count_distinct(TargetUserName)``` |
|` max() `       | Returns the maximum value in the result set or group. | `summarize max(<Expression>)` | ```DevicePerformance \| summarize max(CpuUsage)``` |
|` min()   `     | Returns the minimum value in the result set or group. | `summarize min(<Expression>)` | ```DevicePerformance \| summarize min(MemoryUsage)``` |
|` avg()   `     | Computes the average (mean) of numeric values in the result set or group. | `summarize avg(<NumericExpression>)` | ```DevicePerformance \| summarize avg(CpuUsage)``` |
| `sum()   `     | Calculates the sum of numeric values in the result set or group. | `summarize sum(<NumericExpression>)` | ```DevicePerformance \| summarize sum(DiskUsage)``` |
