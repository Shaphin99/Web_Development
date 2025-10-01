

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Extended SQL Data Types Comparison Cheat Sheet</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        h2 { color: #333; }
        table { width: 100%; border-collapse: collapse; margin-bottom: 40px; page-break-inside: avoid; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
        pre { background-color: #f8f8f8; padding: 10px; border: 1px solid #ddd; overflow: auto; }
        code { font-family: monospace; }
        @media print {
            table { page-break-inside: avoid; }
            pre { white-space: pre-wrap; }
        }
    </style>
</head>
<body>

<h2>🔢 Numeric Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Integer</td><td>INT</td><td>INT</td><td>INTEGER</td><td>Whole numbers without decimals. Common for counting or indexing.</td><td><pre><code class="language-sql">SELECT CAST(123 AS INT);</code></pre></td><td>123</td></tr>
    <tr><td>Small Integer</td><td>SMALLINT</td><td>SMALLINT</td><td>SMALLINT</td><td>Smaller range than INT. Saves space for limited-range values.</td><td><pre><code class="language-sql">SELECT CAST(32000 AS SMALLINT);</code></pre></td><td>32000</td></tr>
    <tr><td>Big Integer</td><td>BIGINT</td><td>BIGINT</td><td>BIGINT</td><td>Stores very large integers. Useful for IDs or large counters.</td><td><pre><code class="language-sql">SELECT CAST(9223372036854775807 AS BIGINT);</code></pre></td><td>9223372036854775807</td></tr>
    <tr><td>Tiny Integer</td><td>TINYINT</td><td>TINYINT</td><td>(Use SMALLINT)</td><td>Very small numbers. Often used for flags or small categories.</td><td><pre><code class="language-sql">SELECT CAST(255 AS TINYINT);</code></pre></td><td>255</td></tr>
    <tr><td>Medium Integer</td><td>MEDIUMINT</td><td>(Use INT)</td><td>(Use INTEGER)</td><td>Medium-range integers, MySQL-specific for optimization.</td><td><pre><code class="language-sql">SELECT CAST(8388607 AS MEDIUMINT);</code></pre></td><td>8388607</td></tr>
    <tr><td>Decimal</td><td>DECIMAL(5,2)</td><td>DECIMAL(5,2)</td><td>NUMERIC(5,2)</td><td>Exact precision for financial or scientific data.</td><td><pre><code class="language-sql">SELECT CAST(123.45 AS DECIMAL(5,2));</code></pre></td><td>123.45</td></tr>
    <tr><td>Float</td><td>FLOAT</td><td>FLOAT</td><td>REAL</td><td>Approximate numeric with floating point. Not ideal for money.</td><td><pre><code class="language-sql">SELECT CAST(123.456 AS FLOAT);</code></pre></td><td>123.456</td></tr>
    <tr><td>Double</td><td>DOUBLE</td><td>FLOAT</td><td>DOUBLE PRECISION</td><td>Higher precision float. Used in scientific calculations.</td><td><pre><code class="language-sql">SELECT CAST(123.456789 AS DOUBLE);</code></pre></td><td>123.456789</td></tr>
    <tr><td>Bit</td><td>BIT</td><td>BIT</td><td>(Use BOOLEAN)</td><td>Stores bit values for binary flags.</td><td><pre><code class="language-sql">SELECT CAST(1 AS BIT);</code></pre></td><td>1</td></tr>
    <tr><td>Money</td><td>(Use DECIMAL)</td><td>MONEY</td><td>MONEY</td><td>Stores currency amounts with fixed precision.</td><td><pre><code class="language-sql">SELECT CAST(123.45 AS MONEY);</code></pre></td><td>123.45</td></tr>
    <tr><td>Small Money</td><td>(Use DECIMAL)</td><td>SMALLMONEY</td><td>(Use MONEY)</td><td>Smaller range currency type.</td><td><pre><code class="language-sql">SELECT CAST(123.45 AS SMALLMONEY);</code></pre></td><td>123.45</td></tr>
    <tr><td>Auto-Increment Small</td><td>(Use SMALLINT AUTO_INCREMENT)</td><td>(Use SMALLINT IDENTITY)</td><td>SMALLSERIAL</td><td>Auto-incrementing small integer.</td><td><pre><code class="language-sql">CREATE TABLE test (id SMALLSERIAL);</code></pre></td><td>(Auto-generated: 1,2,...)</td></tr>
    <tr><td>Auto-Increment</td><td>(Use INT AUTO_INCREMENT)</td><td>(Use INT IDENTITY)</td><td>SERIAL</td><td>Auto-incrementing integer.</td><td><pre><code class="language-sql">CREATE TABLE test (id SERIAL);</code></pre></td><td>(Auto-generated: 1,2,...)</td></tr>
    <tr><td>Auto-Increment Big</td><td>(Use BIGINT AUTO_INCREMENT)</td><td>(Use BIGINT IDENTITY)</td><td>BIGSERIAL</td><td>Auto-incrementing big integer.</td><td><pre><code class="language-sql">CREATE TABLE test (id BIGSERIAL);</code></pre></td><td>(Auto-generated: 1,2,...)</td></tr>
</table>

<h2>🔤 String Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Fixed String</td><td>CHAR(5)</td><td>CHAR(5)</td><td>CHAR(5)</td><td>Fixed-length text. Pads with spaces if shorter.</td><td><pre><code class="language-sql">SELECT CAST('Hi' AS CHAR(5));</code></pre></td><td>'Hi   '</td></tr>
    <tr><td>Variable String</td><td>VARCHAR(10)</td><td>VARCHAR(10)</td><td>VARCHAR(10)</td><td>Flexible-length text. Efficient for varying string sizes.</td><td><pre><code class="language-sql">SELECT CAST('Hello' AS VARCHAR(10));</code></pre></td><td>'Hello'</td></tr>
    <tr><td>Large Text</td><td>TEXT</td><td>TEXT / NTEXT</td><td>TEXT</td><td>Stores long-form text. Not ideal for indexing.</td><td><pre><code class="language-sql">INSERT INTO notes (content) VALUES ('This is a long paragraph...');</code></pre></td><td>(Stored text)</td></tr>
    <tr><td>Unicode</td><td>NVARCHAR(10)</td><td>NVARCHAR(10)</td><td>VARCHAR(10) with UTF-8</td><td>Supports international characters. Ideal for multilingual data.</td><td><pre><code class="language-sql">SELECT CAST(N'नमस्ते' AS NVARCHAR(10));</code></pre></td><td>'नमस्ते'</td></tr>
    <tr><td>Fixed Unicode</td><td>NCHAR(5)</td><td>NCHAR(5)</td><td>CHAR(5) with UTF-8</td><td>Fixed-length Unicode text.</td><td><pre><code class="language-sql">SELECT CAST(N'Hi' AS NCHAR(5));</code></pre></td><td>'Hi   '</td></tr>
    <tr><td>Enum</td><td>ENUM</td><td>(Use VARCHAR CHECK)</td><td>ENUM</td><td>Stores one value from a predefined list.</td><td><pre><code class="language-sql">CREATE TYPE color AS ENUM ('red', 'blue');</code></pre></td><td>'red'</td></tr>
    <tr><td>Set</td><td>SET</td><td>(Use VARCHAR)</td><td>(Use ARRAY)</td><td>Stores zero or more values from a list.</td><td><pre><code class="language-sql">SELECT CAST('red,blue' AS SET('red','blue'));</code></pre></td><td>'red,blue'</td></tr>
</table>

<h2>📅 Date & Time Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Date</td><td>DATE</td><td>DATE</td><td>DATE</td><td>Stores calendar date only. No time component.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30' AS DATE);</code></pre></td><td>2025-09-30</td></tr>
    <tr><td>Time</td><td>TIME</td><td>TIME</td><td>TIME</td><td>Stores time of day. Useful for scheduling.</td><td><pre><code class="language-sql">SELECT CAST('17:30:00' AS TIME);</code></pre></td><td>17:30:00</td></tr>
    <tr><td>DateTime</td><td>DATETIME</td><td>DATETIME</td><td>TIMESTAMP</td><td>Combines date and time. Common for logs and events.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30 17:30:00' AS DATETIME);</code></pre></td><td>2025-09-30 17:30:00</td></tr>
    <tr><td>Timestamp</td><td>TIMESTAMP</td><td>ROWVERSION</td><td>TIMESTAMP</td><td>Auto-updated time. Tracks changes or versioning.</td><td><pre><code class="language-sql">CREATE TABLE logs (updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP);</code></pre></td><td>(Auto-filled timestamp)</td></tr>
    <tr><td>Year</td><td>YEAR</td><td>(Use INT)</td><td>(Use INT)</td><td>Stores year only. Useful for birth years or fiscal data.</td><td><pre><code class="language-sql">SELECT CAST('2025' AS YEAR);</code></pre></td><td>2025</td></tr>
    <tr><td>Small DateTime</td><td>(Use DATETIME)</td><td>SMALLDATETIME</td><td>(Use TIMESTAMP)</td><td>Less precise date/time, smaller range.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30 17:30' AS SMALLDATETIME);</code></pre></td><td>2025-09-30 17:30:00</td></tr>
    <tr><td>DateTime2</td><td>(Use DATETIME)</td><td>DATETIME2</td><td>(Use TIMESTAMP)</td><td>High-precision date/time.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30 17:30:00.1234567' AS DATETIME2);</code></pre></td><td>2025-09-30 17:30:00.1234567</td></tr>
    <tr><td>DateTime Offset</td><td>(Use TIMESTAMP)</td><td>DATETIMEOFFSET</td><td>TIMESTAMPTZ</td><td>Date/time with time zone offset.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30 17:30:00 -05:00' AS DATETIMEOFFSET);</code></pre></td><td>2025-09-30 17:30:00 -05:00</td></tr>
    <tr><td>Time with Time Zone</td><td>(Use TIME)</td><td>(Use TIME)</td><td>TIME WITH TIME ZONE</td><td>Time with time zone.</td><td><pre><code class="language-sql">SELECT CAST('17:30:00 -05:00' AS TIME WITH TIME ZONE);</code></pre></td><td>17:30:00 -05:00</td></tr>
    <tr><td>Timestamp with Time Zone</td><td>(Use TIMESTAMP)</td><td>(Use DATETIMEOFFSET)</td><td>TIMESTAMP WITH TIME ZONE</td><td>Date/time with time zone.</td><td><pre><code class="language-sql">SELECT CAST('2025-09-30 17:30:00 -05:00' AS TIMESTAMP WITH TIME ZONE);</code></pre></td><td>2025-09-30 17:30:00 -05:00</td></tr>
    <tr><td>Interval</td><td>(Use TIME)</td><td>(Use TIME)</td><td>INTERVAL</td><td>Stores time spans or durations.</td><td><pre><code class="language-sql">SELECT INTERVAL '1 day 2 hours';</code></pre></td><td>1 day 02:00:00</td></tr>
</table>

<h2>🔢 Boolean Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Boolean</td><td>(Use TINYINT)</td><td>(Use BIT)</td><td>BOOLEAN</td><td>Stores true/false values.</td><td><pre><code class="language-sql">SELECT CAST(TRUE AS BOOLEAN);</code></pre></td><td>true</td></tr>
</table>

<h2>📦 Binary Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Fixed Binary</td><td>BINARY(10)</td><td>BINARY(10)</td><td>(Use BYTEA)</td><td>Fixed-length binary data.</td><td><pre><code class="language-sql">SELECT CAST(0xDEADBEEF AS BINARY(4));</code></pre></td><td>0xDEADBEEF</td></tr>
    <tr><td>Variable Binary</td><td>VARBINARY(10)</td><td>VARBINARY(10)</td><td>BYTEA</td><td>Variable-length binary data.</td><td><pre><code class="language-sql">SELECT CAST(0xDEADBEEF AS VARBINARY(4));</code></pre></td><td>0xDEADBEEF</td></tr>
</table>

<h2>📂 Large Object Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Tiny Text/Blob</td><td>TINYTEXT / TINYBLOB</td><td>(Use VARCHAR(MAX))</td><td>(Use TEXT / BYTEA)</td><td>Small large objects, up to 255 bytes.</td><td><pre><code class="language-sql">INSERT INTO data (blob_col) VALUES (0xFF);</code></pre></td><td>(Stored binary)</td></tr>
    <tr><td>Medium Text/Blob</td><td>MEDIUMTEXT / MEDIUMBLOB</td><td>(Use VARCHAR(MAX))</td><td>(Use TEXT / BYTEA)</td><td>Medium large objects, up to 16MB.</td><td><pre><code class="language-sql">INSERT INTO data (blob_col) VALUES ('Large data...');</code></pre></td><td>(Stored data)</td></tr>
    <tr><td>Long Text/Blob</td><td>LONGTEXT / LONGBLOB</td><td>(Use VARCHAR(MAX))</td><td>(Use TEXT / BYTEA)</td><td>Large objects, up to 4GB.</td><td><pre><code class="language-sql">INSERT INTO data (blob_col) VALUES ('Very large data...');</code></pre></td><td>(Stored data)</td></tr>
    <tr><td>Image</td><td>(Use BLOB)</td><td>IMAGE (deprecated)</td><td>(Use BYTEA)</td><td>Stores binary images (deprecated in SQL Server).</td><td><pre><code class="language-sql">INSERT INTO images (img) VALUES (0xFFD8FF...);</code></pre></td><td>(Stored image binary)</td></tr>
</table>

<h2>🌍 Spatial Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>Point</td><td>POINT</td><td>GEOMETRY</td><td>POINT</td><td>Stores a geometric point.</td><td><pre><code class="language-sql">SELECT ST_PointFromText('POINT(1 2)');</code></pre></td><td>POINT(1 2)</td></tr>
    <tr><td>Line</td><td>LINESTRING</td><td>GEOMETRY</td><td>LINE</td><td>Stores a line or line string.</td><td><pre><code class="language-sql">SELECT ST_LineFromText('LINESTRING(0 0,1 1)');</code></pre></td><td>LINESTRING(0 0,1 1)</td></tr>
    <tr><td>Polygon</td><td>POLYGON</td><td>GEOMETRY</td><td>POLYGON</td><td>Stores a polygon shape.</td><td><pre><code class="language-sql">SELECT ST_PolygonFromText('POLYGON((0 0,1 0,1 1,0 1,0 0))');</code></pre></td><td>POLYGON((0 0,1 0,1 1,0 1,0 0))</td></tr>
    <tr><td>Geography</td><td>(Use SPATIAL)</td><td>GEOGRAPHY</td><td>(Use GEOMETRY with SRID)</td><td>Stores geographic data (e.g., earth coordinates).</td><td><pre><code class="language-sql">SELECT geography::STGeomFromText('POINT(-122.35 47.62)', 4326);</code></pre></td><td>POINT(-122.35 47.62)</td></tr>
</table>

<h2>📄 JSON / XML Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>JSON</td><td>JSON</td><td>(Use NVARCHAR(MAX))</td><td>JSON</td><td>Stores JSON documents.</td><td><pre><code class="language-sql">SELECT CAST('{"key": "value"}' AS JSON);</code></pre></td><td>{"key": "value"}</td></tr>
    <tr><td>JSON Binary</td><td>(Use JSON)</td><td>(Use NVARCHAR(MAX))</td><td>JSONB</td><td>Binary-optimized JSON for faster querying.</td><td><pre><code class="language-sql">SELECT CAST('{"key": "value"}' AS JSONB);</code></pre></td><td>{"key": "value"}</td></tr>
    <tr><td>XML</td><td>(Use TEXT)</td><td>XML</td><td>XML</td><td>Stores XML documents.</td><td><pre><code class="language-sql">SELECT CAST('<root><key>value</key></root>' AS XML);</code></pre></td><td><root><key>value</key></root></td></tr>
</table>

<h2>🛠 Miscellaneous Types</h2>
<table>
    <tr><th>Concept</th><th>MySQL</th><th>SQL Server</th><th>PostgreSQL</th><th>Description</th><th>Example Code</th><th>Output</th></tr>
    <tr><td>UUID</td><td>(Use CHAR(36))</td><td>UNIQUEIDENTIFIER</td><td>UUID</td><td>Stores universally unique identifiers.</td><td><pre><code class="language-sql">SELECT UUID();</code></pre></td><td>e.g., a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11</td></tr>
    <tr><td>Array</td><td>(Use JSON)</td><td>(Use TABLE)</td><td>ARRAY</td><td>Stores arrays of values.</td><td><pre><code class="language-sql">SELECT ARRAY[1,2,3];</code></pre></td><td>{1,2,3}</td></tr>
    <tr><td>Network Address</td><td>(Use VARCHAR)</td><td>(Use VARCHAR)</td><td>INET / CIDR</td><td>Stores IP addresses or networks.</td><td><pre><code class="language-sql">SELECT CAST('192.168.1.1' AS INET);</code></pre></td><td>192.168.1.1</td></tr>
    <tr><td>Composite</td><td>(Use Multiple Columns)</td><td>(Use TABLE)</td><td>COMPOSITE</td><td>User-defined composite types.</td><td><pre><code class="language-sql">CREATE TYPE complex AS (r real, i real);</code></pre></td><td>(1.0, 2.0)</td></tr>
    <tr><td>Hierarchy ID</td><td>(Use Nested Sets)</td><td>HIERARCHYID</td><td>(Use LTREE extension)</td><td>Stores hierarchical data.</td><td><pre><code class="language-sql">SELECT CAST('/1/2/' AS HIERARCHYID);</code></pre></td><td>/1/2/</td></tr>
    <tr><td>SQL Variant</td><td>(Use VARCHAR)</td><td>SQL_VARIANT</td><td>(Use ANY)</td><td>Stores data of various types.</td><td><pre><code class="language-sql">DECLARE @var SQL_VARIANT = 123;</code></pre></td><td>123</td></tr>
</table>

</body>
</html>
```

This HTML is ready for printing and maintains the code theme through structured <pre><code> elements. If you need further customizations, such as adding CSS for colors or adjusting table widths, let me know.

**Key Citations:**
- [SQL Data Types: Oracle, SQL Server, MySQL, PostgreSQL](https://www.databasestar.com/sql-data-types/)
- [Data types (Transact-SQL) - SQL Server](https://learn.microsoft.com/en-us/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-ver17)
- [MySQL :: MySQL 8.4 Reference Manual :: 13 Data Types](https://dev.mysql.com/doc/refman/8.4/en/data-types.html)
- [Chapter 8. Data Types](https://www.postgresql.org/docs/current/datatype.html)
