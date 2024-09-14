<img src ="https://github.com/user-attachments/assets/ebef05b3-f58d-463a-8d9a-4679fd357359" width="100">

# Splunk Overview

Splunk is an event management system (SIEM) that helps you make sense of large amounts of data, find problems, and understand what’s happening in your digital environment. This gives better view over the network, ability to hunt for threats, and respond to incidents. 

## Adding data example below:


![Screenshot 2024-09-14 at 4 03 57 PM](https://github.com/user-attachments/assets/a125df1b-e486-4bab-a06d-c165c1a0d6fa)






## Key Concepts

### Sourcetype
It is a key piece of information (metadata field) used by Splunk to parse and extract fields from the raw data and apply appropriate data models, tags, and other settings.  This data can consist of Windows Event logs, Sysmon  Logs, Fortinet Firewall Log, Suricata logs, etc. When data is ingested into Splunk, it is assigned a sourcetype based on its source and format, such as:
- `access_combined` for Apache logs
- `syslog` for system logs
- `JSON` for structured data

### Splunk Main Functions:


1. Index
2. Search and Investigate
3. Add Knowledge
4. Monitor and Alert
5. Report and Analyze

### Indexing 
When data is added to Splunk, it is first indexed. This involves breaking it into individual events, parsing out relevant fields, and assigning timestamps and other metadata. The Splunk indexing engine uses a multi-step process:

1. Breaking the data into events.
2. Parsing the events to extract fields.
3. Normalizing the fields into a common format.
4. Storing the normalized events in an index.

NOTE: Bucketing manages index file

## Components

### Search Head
The search head is a component of Splunk that enables users to search and analyze data in real time. When a user initiates a search query, it is sent to the search head, which then distributes the search to one or more indexers. This is the User Interface (UI) Some functions include SPL, Real-time searching, visualization and correlation.

### Forwarder
The forwarder is a component of Splunk responsible for collecting and forwarding data from various sources to the Splunk indexers. Universal = `lightweight` , Heavy = `Full`

## Field Removal


- `-<field>`: Removes all of the fields.
<img width="955" alt="1" src="https://github.com/user-attachments/assets/65199e63-c554-4199-8409-6cb9f37e65df">

- `- <field>`: Removes a particular field.
<img width="954" alt="2" src="https://github.com/user-attachments/assets/e2e6cda2-9714-481b-9e52-db4b2170fba1">

## Key Concepts

<img width="960" alt="general" src="https://github.com/user-attachments/assets/f66756ee-fe05-469b-a902-b51fc1519f1a">






1. **Key-Value Pairs**: Represent structured data in events and are formatted as `<key>=<value>`.
2. **Wildcard Value**: In Splunk, the asterisk (`*`) character is used as a wildcard to match unlimited values.
3. **Events, Patterns, Stats, Visuals**: 
   - An event refers to a single line of data containing timestamped data along with any other relevant information.
4. **Search Modes**:
   - **Fast Mode**: Designed to return search results as quickly as possible, sacrificing some accuracy and completeness for speed.
   - **Smart Mode**: Automatically switches between Fast and Verbose modes depending on the search size and complexity. It attempts to balance speed and accuracy and is the default search mode in Splunk.
   - **Verbose Mode**: Provides the most accurate and complete search results, even if it takes longer to execute. It performs a detailed analysis of all events in the data, useful for debugging and troubleshooting purposes.
5. **Timeline**: The timeline is a visual representation of the number of events in your search results that occur at each point in time. It shows the distribution of events over time. When searching or saving a search, you can specify absolute and relative time ranges using time modifiers:
   - **Absolute Time Range**: Uses specific dates and times (e.g., from 12 A.M. April 1, 2023 to 12 A.M. April 13, 2023).
   - **Relative Time Range**: Dependent on when the search is run. For example, a relative time range of `-60m` means 60 minutes ago. If the current time is 3 P.M., the search will cover the past 60 minutes.

## Running Basic Searches
**Example**:
- The value is not case-sensitive. Therefore, `sourcetype=LiNux_SECUre` and `sourcetype=linux_secure` would be the same
  
<img width="942" alt="general2incase" src="https://github.com/user-attachments/assets/8172e486-8a19-46d1-8aca-2bac8cb805bd">

In Splunk, key-value pairs are used to represent structured data in the events being indexed. Each key-value pair is separated by an equal sign (`=`), and each pair is separated by a space or a comma. 

**Example**:
- In a log event, the key could be `sourcetype` and the value could be `linux_secure`, represented as `sourcetype=linux_secure` in Splunk.
- The key is case-sensitive (e.g., `Sourcetype` and `Host` are not the same as `sourcetype` and `host`, so no value would be returned if mismatched). 

<img width="946" alt="casesentigeneral" src="https://github.com/user-attachments/assets/32838089-0a08-4916-844c-f55bbbe23cf6">


## Search Categories
1. Search Terms
2. Commands
3. Functions
4. Arguments 
5. Clauses 

## Saving Searches

Saving a search, whether as a report, alert, or dashboard, preserves and shares a predefined view of data extracted and analyzed from a search query. You can also export search results to a file in the following formats:
- Raw events
- CSV
- XML
- JSON


## Event Viewer
Display option `List`, `Raw` and `Table`
List has `3` columns `/`  `Time` and `Event`

## Splunk Apps
Built and Certified are by Splunk ; can dowload in Splunk or at `Spunkbase.com`
Stored - `C:\Program Files\Splunk\etc\apps\[app name] folder`

## Deployment Types
`Standaline`, `Distributed` and `Cloud`

## Custom Knowledge
`Custom fields`, `Tags`, `Lookups`

## Transforming Commands
`top`, `rare` and `stats`

## Machine Data
Machine data refers to data generated by machines, systems, or devices. This data is often produced automatically and in large quantities, making it difficult to manage and analyze without the right tools. Examples include:
- **Server logs**: Information about server events such as user logins, system errors, and software updates.

## Fields
Fields are searchable name/value pairings in event data. They represent key/value pairs, for example:
- `host=www2`
- `status=200`

### Common Fields
- `host`: Indicates the hostname or IP address of the machine where the event originated.
- `source`: Specifies the input source or file from which the event was read.
- `sourcetype`: Identifies the type or format of the data source, such as a log file or network data.
- `index`: Represents the index in which the event is stored.

### Basic Default Fields
- `linecount`
- `punct`
- `splunk_server`
- `timestamp`

## Pipeline
The search pipeline involves chaining commands using the pipe symbol (`|`) to pass results from one command to the next. For example:
```spl
index=games sourcetype="SimCubeBeta" | top host | fields - percent
```

## Timeline
Time range is specified with `Time Range Picker`

For `exact time ranges`, the syntax for the time modifiers is `%m/%d/%Y:%H:%M:%S.` 
ex. `earliest=04/19/2023:00:00:00 latest=04/27/2023:00:00:00`
Search can be `absolute` or `relative` . 
Absolute is specific time and dates
Relative is depending on when search is ran
Current time = `now`
Set start with `earliest=` and set end with `latest=` 
Separate the time amount from the snap to time unit with an `"@"` character.


## Control Job Search
`Edit`, `Send`, `Inspect` and `Delete`
Default lifetime is `10 minutes` can extend to `7 days`



## Pipelining
The first intermediate results table shows events retrieved from the index that matched the
search terms `sourcetype=SimCubeBeta.`
The second intermediate results table shows the results of the `top` command, "top host,"
summarizing the events into a list of the top 10 users, the user count, and percentage.`
The "fields - percent" removes the column that shows the percentage; therefore, you are
left with a smaller final results table


It involves chaining together multiple commands using the pipe symbol (|) to pass
the results from one command to the next.

# Common Search Commands

| Command       | Description                                                    |
|---------------|----------------------------------------------------------------|
| `chart/ timechart` | Returns results in a tabular output for (time-series) charting. |
| `dedup`       | Removes subsequent results that match a specified criterion.  |
| `eval`        | Calculates an expression. See [COMMON EVAL FUNCTIONS](#common-eval-functions). |
| `fields`      | Removes fields from search results.                           |
| `head/tail`   | Returns the first/last N results.                             |
| `lookup`      | Adds field values from an external source.                    |
| `rename`      | Renames a field. Use wildcards to specify multiple fields.    |
| `rex`         | Specifies regular expression named groups to extract fields. |
| `search`      | Filters results to those that match the search expression.    |
| `sort`        | Sorts the search results by the specified fields.             |
| `stats`       | Provides statistics, grouped optionally by fields. See [COMMON STATS FUNCTIONS](#common-stats-functions). |
| `mstats`      | Similar to stats but used on metrics instead of events.        |
| `table`       | Specifies fields to keep in the result set. Retains data in tabular format. |
| `top/rare`    | Displays the most/least common values of a field.              |
| `transaction` | Groups search results into transactions.                      |
| `where`       | Filters search results using eval expressions. Used to compare two different fields. |

## Common Eval Functions

The `eval` command calculates an expression and puts the resulting value into a field (e.g., `...| eval force = mass * acceleration`). The following table lists some of the functions used with the `eval` command. You can also use basic arithmetic operators (`+ - * / %`), string concatenation (e.g., `...| eval name = last . "," . first`), and Boolean operations (`AND OR NOT XOR < > <= >= != = == LIKE`).

| Function             | Description                                                       | Examples                                              |
|----------------------|-------------------------------------------------------------------|-------------------------------------------------------|
| `abs(X)`             | Returns the absolute value of X.                                 | `abs(number)`                                        |
| `case(X,"Y",…)`      | Takes pairs of arguments X and Y, where X arguments are Boolean expressions. When evaluated to TRUE, the arguments return the corresponding Y argument. | `case(error == 404, "Not found", error == 500, "Internal Server Error", error == 200, "OK")` |
| `ceil(X)`            | Ceiling of a number X.                                           | `ceil(1.9)`                                          |
| `cidrmatch("X",Y)`   | Identifies IP addresses that belong to a particular subnet.      | `cidrmatch("123.132.32.0/25",ip)`                    |
| `coalesce(X,…)`      | Returns the first value that is not null.                        | `coalesce(null(), "Returned val", null())`           |
| `cos(X)`             | Calculates the cosine of X.                                      | `n=cos(0)`                                           |
| `exact(X)`           | Evaluates an expression X using double precision floating point arithmetic. | `exact(3.14*num)`                                    |
| `exp(X)`             | Returns e^X.                                                      | `exp(3)`                                             |
| `if(X,Y,Z)`          | If X evaluates to TRUE, the result is the second argument Y. If X evaluates to FALSE, the result evaluates to the third argument Z. | `if(error==200, "OK", "Error")`                      |
| `in(field,valuelist)`| Returns TRUE if a value in "value-list" matches a value in "field". You must use the “in” function inside the “if” function. | `if(in(status, “404”,”500”,”503”),”true”,”false”)` |
| `isbool(X)`          | Returns TRUE if X is Boolean.                                    | `isbool(field)`                                      |
| `isint(X)`           | Returns TRUE if X is an integer.                                 | `isint(field)`                                       |
| `isnull(X)`          | Returns TRUE if X is NULL.                                      | `isnull(field)`                                      |
| `isstr()`            | Returns TRUE if X is a string.                                   | `isstr(field)`                                       |
| `len(X)`             | This function returns the character length of a string X.        | `len(field)`                                         |
| `like(X,"Y")`        | Returns TRUE if and only if X is like the SQLite pattern in Y.   | `like(field, "addr%")`                               |
| `log(X,Y)`           | Returns the log of the first argument X using the second argument Y as the base. Y defaults to 10. | `log(number,2)`                                      |
| `lower(X)`           | Returns the lowercase of X.                                      | `lower(username)`                                    |
| `ltrim(X,Y)`         | Returns X with the characters in Y trimmed from the left side. Y defaults to spaces and tabs. | `ltrim(" ZZZabcZZ ", " Z")`                          |
| `match(X,Y)`         | Returns if X matches the regex pattern Y.                        | `match(field, "^\d{1,3}\.\d$")`                      |
| `max(X,…)`           | Returns the maximum.                                             | `max(delay, mydelay)`                                |
| `md5(X)`             | Returns the MD5 hash of a string value X.                        | `md5(field)`                                         |
| `min(X,…)`           | Returns the minimum.                                             | `min(delay, mydelay)`                                |
| `mvcount(X)`         | Returns the number of values of X.                               | `mvcount(multifield)`                                |
| `mvfilter(X)`        | Filters a multi-valued field based on the Boolean expression X.  | `mvfilter(match(email, "net$"))`                     |
| `mvindex(X,Y,Z)`     | Returns a subset of the multivalued field X from start position (zero-based) Y to Z (optional). | `mvindex(multifield, 2)`                              |
| `mvjoin(X,Y)`        | Given a multi-valued field X and string delimiter Y, and joins the individual values of X using Y. | `mvjoin(address, ";")`                               |
| `now()`              | Returns the current time, represented in Unix time.              | `now()`                                              |
| `null()`             | This function takes no arguments and returns NULL.               | `null()`                                             |
| `nullif(X,Y)`        | Given two arguments, fields X and Y, and returns the X if the arguments are different. Otherwise returns NULL. | `nullif(fieldA, fieldB)`                              |
| `random()`           | Returns a pseudo-random number ranging from 0 to 2147483647.     | `random()`                                           |
| `relative_time(X,Y)` | Given epochtime time X and relative time specifier Y, returns the epochtime value of Y applied to X. | `relative_time(now(),"-1d@d")`                        |
| `replace(X,Y,Z)`     | Returns a string formed by substituting string Z for every occurrence of regex string Y in string X. | `replace(date,"^(\d{1,2})/(\d{1,2})/", "\2/\1/")`  |
| `round(X,Y)`         | Returns X rounded to the amount of decimal places specified by Y. The default is to round to an integer. | `round(3.5)`                                         |
| `rtrim(X,Y)`         | Returns X with the characters in Y trimmed from the right side. If Y is not specified, spaces and tabs are trimmed. | `rtrim(" ZZZZabcZZ ", " Z")`                         |
| `split(X,Y)`         | Returns X as a multi-valued field, split by delimiter Y.          | `split(address, ";")`                                |
| `sqrt(X)`            | Returns the square root of X.                                   | `sqrt(9)`                                            |
| `strftime(X,Y)`      | Returns epochtime value X rendered using the format specified by Y. | `strftime(_time, "%H:%M")`                           |
| `strptime(X,Y)`      | Given a time represented by a string X, returns value parsed from format Y. | `strptime(timeStr, "%H:%M")`                         |
| `substr(X,Y,Z)`      | Returns a substring field X from start position (1-based) Y for Z (optional) characters. | `substr("string", 1, 3)`                             |
| `time()`             | Returns the wall-clock time with microsecond resolution.         | `time()`                                             |
| `tonumber(X,Y)`      | Converts input string X to a number, where Y (optional, defaults to 10) defines the base of the number to convert to. | `tonumber("0A4",16)`                                 |
| `tostring(X,Y)`      | Returns a field value of X as a string. If the value of X is a number, it reformats it as a string. If X is a Boolean value, it reformats to "True" or "False". If X is a number, the second argument Y is optional and can either be "hex" (convert X to hexadecimal), "commas" (formats X with commas and 2 decimal places), or "duration"


# Common Stats Functions

Common statistical functions used with the `chart`, `stats`, and `timechart` commands. Field names can be wildcarded, so `avg(*delay)` might calculate the average of the `delay` and `xdelay` fields.

## Statistical Functions

- **`avg(X)`**  
  Returns the average of the values of field `X`.

- **`count(X)`**  
  Returns the number of occurrences of the field `X`. To indicate a specific field value to match, format `X` as `eval(field="value")`.

- **`dc(X)`**  
  Returns the count of distinct values of the field `X`.

- **`earliest(X)`**  
  Returns the chronologically earliest seen value of `X`.

- **`latest(X)`**  
  Returns the chronologically latest seen value of `X`.

- **`max(X)`**  
  Returns the maximum value of the field `X`. If the values of `X` are non-numeric, the max is found from alphabetical ordering.

- **`median(X)`**  
  Returns the middle-most value of the field `X`.

- **`min(X)`**  
  Returns the minimum value of the field `X`. If the values of `X` are non-numeric, the min is found from alphabetical ordering.

- **`mode(X)`**  
  Returns the most frequent value of the field `X`.

- **`perc<X>(Y)`**  
  Returns the X-th percentile value of the field `Y`. For example, `perc5(total)` returns the 5th percentile value of a field "total".

- **`range(X)`**  
  Returns the difference between the max and min values of the field `X`.

- **`stdev(X)`**  
  Returns the sample standard deviation of the field `X`.

- **`stdevp(X)`**  
  Returns the population standard deviation of the field `X`.

- **`sum(X)`**  
  Returns the sum of the values of the field `X`.

- **`sumsq(X)`**  
  Returns the sum of the squares of the values of the field `X`.

- **`values(X)`**  
  Returns the list of all distinct values of the field `X` as a multi-value entry. The order of the values is alphabetical.

- **`var(X)`**  
  Returns the sample variance of the field `X`.

## Search Examples

- **Filter Results**  
  Returns `X` rounded to the amount of decimal places specified by `Y`. The default is to round to an integer.  
  Example: `round(3.5)`

- **Trim Right Characters**  
  Returns `X` with the characters in `Y` trimmed from the right side. If `Y` is not specified, spaces and tabs are trimmed.  
  Example: `rtrim(" ZZZZabcZZ ", " Z")`

- **Split Field**  
  Returns `X` as a multi-valued field, split by delimiter `Y`.  
  Example: `split(address, ";")`
