<img src ="https://github.com/user-attachments/assets/ebef05b3-f58d-463a-8d9a-4679fd357359" width="100">

# Splunk Overview

Splunk is an event management system (SIEM) that helps you make sense of large amounts of data, find problems, and understand what’s happening in your digital environment.


## Key Concepts

### Sourcetype
It is a key piece of information used by Splunk to parse and extract fields from the raw data and apply appropriate data models, tags, and other settings. When data is ingested into Splunk, it is assigned a sourcetype based on its source and format, such as:
- `access_combined` for Apache logs
- `syslog` for system logs
- `JSON` for structured data

### Indexing
When data is added to Splunk, it is first indexed. This involves breaking it into individual events, parsing out relevant fields, and assigning timestamps and other metadata. The Splunk indexing engine uses a multi-step process:
1. Breaking the data into events.
2. Parsing the events to extract fields.
3. Normalizing the fields into a common format.
4. Storing the normalized events in an index.
## Components

### Search Head
The search head is a component of Splunk that enables users to search and analyze data in real time. When a user initiates a search query, it is sent to the search head, which then distributes the search to one or more indexers.

### Forwarder
The forwarder is a component of Splunk responsible for collecting and forwarding data from various sources to the Splunk indexers.

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


## Saving Searches

Saving a search, whether as a report, alert, or dashboard, preserves and shares a predefined view of data extracted and analyzed from a search query. You can also export search results to a file in the following formats:
- Raw events
- CSV
- XML
- JSON
### Search Head
The search head is a component of Splunk that enables users to search and analyze data in real time. When a user initiates a search query, it is sent to the search head, which then distributes the search to one or more indexers.

### Forwarder
The forwarder is responsible for collecting and forwarding data from various sources to the Splunk indexers.

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


## Pipelining
The first intermediate results table shows events retrieved from the index that matched the
search terms `sourcetype=SimCubeBeta.`
The second intermediate results table shows the results of the `top` command, "top host,"
summarizing the events into a list of the top 10 users, the user count, and percentage.`
The "fields - percent" removes the column that shows the percentage; therefore, you are
left with a smaller final results table


It involves chaining together multiple commands using the pipe symbol (|) to pass
the results from one command to the next.

