# Datilo.app - Local CSV & XLSX Database Viewer

## Complete Local Processing & Privacy

**Datilo.app** is a powerful, browser-based CSV and Excel file viewer and analyzer that runs entirely in your browser. Your data never leaves your computer - no servers, no uploads, no privacy concerns.

## Key Features

### Complete Local Processing
- **Zero server dependency** - works entirely in your browser
- **Offline capable** - disconnect from internet after loading the page
- **No data transmission** - your files stay on your device
- **No registration required** - just open and use

### Powerful Data Analysis with SQL
- **Full SQLite support** - Use complete SQL syntax to query your data
- **Cross-table queries** - JOIN data between multiple CSV/Excel files
- **Each file becomes a table** - Load multiple files and query them independently
- **Complex analysis** - Aggregate functions, subqueries, window functions, and more
- **Real-time results** - Instant query execution with live results

### Multi-Format File Support
- **CSV files** - All delimiter types, quoted fields, escaped characters
- **Excel files (.xlsx)** - Multiple sheets supported as separate tables
- **Large file support** - Handles files up to 200MB+ through intelligent chunking
- **Smart parsing** - Automatic detection of data types and formats
- **Multiple file loading** - Load and work with dozens of files simultaneously

### Performance Optimized
- **Chunked processing** - breaks large files into manageable pieces
- **Memory efficient** - optimized for browser memory constraints
- **Fast rendering** - displays thousands of rows with smooth scrolling
- **Intelligent pagination** - responsive interface even with massive datasets

### Built-in Database Engine
- **SQLite in browser** - full SQL database functionality without installation
- **Persistent storage** - your data persists between sessions (locally)
- **Export capabilities** - download query results as CSV or Excel
- **Schema inspection** - view table structures and column types

## Use Cases

### Data Analysis & Business Intelligence
- **Sales analysis** - Load sales.csv and customers.xlsx, JOIN them for comprehensive reports
- **Financial reporting** - Combine multiple Excel sheets with SQL aggregations
- **Data validation** - Cross-reference data between different sources
- **Trend analysis** - Use SQL window functions for time-series analysis

### Privacy-First Processing
- **Sensitive data** - Process confidential information without cloud exposure
- **Compliance** - Meet data protection requirements with local-only processing
- **Offline analysis** - Work with data in air-gapped environments

### Education & Learning
- **SQL training** - Learn SQL with real datasets in a safe environment
- **Data science** - Practice data manipulation without database setup
- **Research** - Analyze research data with full SQL capabilities

## SQL Query Examples

### Single Table Analysis
```sql
-- Analyze sales data
SELECT product, SUM(amount) as total_sales 
FROM sales_data 
GROUP BY product 
ORDER BY total_sales DESC;
```

### Cross-Table Joins
```sql
-- Combine customer data with orders
SELECT c.customer_name, SUM(o.order_value) as total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_name
HAVING total_spent > 1000;
```

### Advanced Analytics
```sql
-- Monthly growth analysis
SELECT 
    strftime('%Y-%m', order_date) as month,
    SUM(amount) as monthly_total,
    LAG(SUM(amount)) OVER (ORDER BY strftime('%Y-%m', order_date)) as prev_month,
    ROUND((SUM(amount) - LAG(SUM(amount)) OVER (ORDER BY strftime('%Y-%m', order_date))) * 100.0 / LAG(SUM(amount)) OVER (ORDER BY strftime('%Y-%m', order_date)), 2) as growth_percent
FROM sales
GROUP BY strftime('%Y-%m', order_date)
ORDER BY month;
```

## Quick Start

1. **Open the application** in any modern web browser
2. **Load your data**:
   - Drag & drop CSV files or Excel (.xlsx) files
   - Or click "Select CSV/Excel" to browse files
   - Each file becomes an independent table
3. **Configure if needed** - separators are auto-detected
4. **Start querying**:
   - Use the SQL editor to write queries
   - Reference tables by their filename (without extension)
   - JOIN multiple tables for cross-analysis

## How It Works

Datilo.app transforms your browser into a complete database environment:

- **SQL.js** - SQLite compiled to WebAssembly for in-browser database
- **File API** - Direct file access without server uploads
- **SheetJS** - Excel file parsing for .xlsx support
- **Web Workers** - Background processing for responsive UI
- **IndexedDB** - Local storage for persistence across sessions

## Table Management

### File to Table Mapping
- `sales_data.csv` becomes table `sales_data`
- `customers.xlsx` becomes table `customers`
- Multi-sheet Excel files create multiple tables: `workbook_sheet1`, `workbook_sheet2`

### Cross-File Analysis
Load multiple files and query them together:
```sql
-- Analyze data across three different files
SELECT 
    p.product_name,
    s.total_sales,
    i.current_inventory
FROM products p
JOIN (SELECT product_id, SUM(quantity) as total_sales FROM sales GROUP BY product_id) s 
    ON p.product_id = s.product_id
JOIN inventory i ON p.product_id = i.product_id
WHERE i.current_inventory < 100;
```

## Browser Requirements

- **Chrome/Edge** 88+ (Recommended)
- **Firefox** 85+
- **Safari** 14+
- **Opera** 74+

*Requires JavaScript enabled and modern browser features (FileReader API, WebAssembly)*

## Privacy & Security

### What Datilo.app Does
- Processes files entirely in your browser
- Stores data locally using browser storage APIs
- Uses HTTPS for secure page delivery
- Implements Content Security Policy

### What Datilo.app Does NOT Do
- Upload your files to any server
- Send data to third parties
- Require user accounts or login
- Track user behavior or analytics
- Store files on external services

## Contributing

We welcome bug reports, feature requests, and feedback!

### Report Issues
- **Bug Reports**: [Create an issue](https://github.com/Gus1no/datiloapp/issues/new?template=bug_report.md)
- **Feature Requests**: [Request a feature](https://github.com/Gus1no/datiloapp/issues/new?template=feature_request.md)
- **Questions**: [Start a discussion](https://github.com/Gus1no/datiloapp/discussions)

## Support

- **Website**: [datilo.app](https://datilo.app)
- **GitHub Issues**: [Report bugs or request features](https://github.com/Gus1no/datiloapp/issues)
- **Discussions**: [Community support](https://github.com/Gus1no/datiloapp/discussions)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **SQL.js** - SQLite compiled to JavaScript
- **SheetJS** - Excel file processing library
- **Feather Icons** - Beautiful open-source icons
- **Browser vendors** - For providing powerful web APIs
