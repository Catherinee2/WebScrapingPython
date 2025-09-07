# Web Scraping Project: Largest US Companies by Revenue (Python)

## **Project Overview**
This project demonstrates the process of **web scraping** data from a real website (Wikipedia) using **Python** to extract structured information. The goal was to pull a list of the largest companies in the United States by **revenue**, including their **rank, name, industry, and other key details**, and then organize this data into a **Pandas DataFrame** and optionally export it to a CSV file.

## **Problem Statement & Objectives**
The primary objective was to extract specific tabular data from a Wikipedia web page. This involved overcoming challenges typical of real-world web scraping, such as:

- Identifying and isolating the correct target table from potentially multiple tables on a single page.
- Properly parsing HTML elements (**headers and row data**).
- Cleaning extracted text by removing unwanted characters like `\n` (newline characters).
- Structuring the scraped data into a **clean and usable Pandas DataFrame**.
- Debugging common issues like **mismatched column counts** when appending rows to a DataFrame.
- Ensuring the clean export of data to a **CSV file** without extraneous index columns.

## **Data Source**
The data was scraped from a Wikipedia web page [U.S. Companies by Revenue on Wikipedia](https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue). This page contained tabular information about companies, including:

- Rank  
- Name  
- Industry  
- Revenue  
- Headquarters  ....

## **Tools Used**
- **Python 3**: Primary programming language for the project.  
- **requests library**: For making HTTP requests to fetch HTML content of the target URL.  
- **BeautifulSoup (from bs4)**: To parse HTML content and navigate the document tree for extracting data.  
- **pandas library**: For creating and manipulating the DataFrame, providing a structured format for the extracted data.  

## **Methodology / Steps Taken**
The project followed a systematic approach for web scraping and data processing:

1. **Library Imports**  
   - Imported `requests`, `BeautifulSoup` from `bs4`, and `pandas` as `pd`.

2. **URL Definition & HTML Fetching**  
   - Defined the Wikipedia URL containing the target data.  
   - Used `requests.get()` to send an HTTP GET request to the URL and obtained the page's HTML content, verifying a successful (200) response.

3. **HTML Parsing**  
   - Initialized a `BeautifulSoup` object with the fetched HTML text and an `html.parser`.

4. **Target Table Identification**  
   - Inspected the web page's HTML to understand its structure and identify the desired table.  
   - Initially used `soup.find('table')` but it retrieved an incorrect table.  
   - Switched to `soup.find_all('table')` to get a list of all tables.  
   - Correct table was found at **index 1** of the `find_all` list.  

5. **Header Extraction**  
   - Table headers were within `<th>` tags.  
   - Extracted all `<th>` tags and used list comprehension to `.text.strip()` each header.  
   - Stored cleaned headers in a list named `world_table_titles` (e.g., Rank, Name, Industry, Revenue).

6. **DataFrame Initialization**  
   - Created an empty Pandas DataFrame: `pd.DataFrame(columns=world_table_titles)`.

7. **Row Data Extraction & DataFrame Population**  
   - Table rows were within `<tr>` tags and individual cells within `<td>` tags.  
   - Iterated through `<tr>` tags starting from **index 1** to skip headers.  
   - Extracted and cleaned text from each `<td>` using `.text.strip()`.  
   - Appended each row to the DataFrame using `df.loc[len(df)] = individual_row_data`.

8. **CSV Export (Optional)**  
   - Exported the final DataFrame using `df.to_csv('filename.csv', index=False)` to avoid extra index columns.

## **Key Results & Insights**
The project successfully demonstrated an **end-to-end web scraping workflow**, delivering a structured dataset:

- **Comprehensive Data Extraction**: All relevant information from the Wikipedia table, including Rank, Name, Industry, Revenue, Revenue Growth, Employees, and Headquarters, was accurately scraped.  
- **Clean & Structured Data**: Organized into a Pandas DataFrame with correctly named columns and cleaned text.  
- **Robust Scraping Techniques**: Demonstrated handling of multiple tables, using `find_all` and indexing for precise targeting.  
- **Effective Data Cleaning**: Used `.strip()` to remove newline characters and ensure clean text.  
- **Problem-Solving**: Addressed common issues like irrelevant tables, empty rows, and CSV index column problems.  
- **Exportable Output**: The dataset can be easily exported to CSV for further analysis.

## **Technical Skills Demonstrated**
- **Web Scraping Fundamentals**: Using Python libraries (`requests`, `BeautifulSoup`) to fetch and parse HTML.  
- **HTML Structure Navigation**: Inspecting and targeting specific tags (`<table>`, `<th>`, `<tr>`, `<td>`).  
- **Data Extraction & Cleaning**: Extracting text from HTML and cleaning it for DataFrame usage.  
- **Python Programming**: Loops, list comprehensions, and conditional logic for efficient data processing.  
- **Pandas DataFrame Manipulation**:  
  - Creating DataFrames with predefined columns.  
  - Dynamically appending rows using `.loc`.  
  - Debugging population issues.  
- **File I/O**: Exporting structured data to CSV (`df.to_csv()`) with proper formatting.  
- **Debugging & Problem Solving**: Iterative troubleshooting for web scraping and data structuring issues.

## **Future Enhancements**
- Automate scraping for multiple pages or updated Wikipedia data.  
- Integrate additional data sources (e.g., financial reports) for richer analysis.  
- Visualize trends using **Matplotlib** or **Seaborn**.  
- Develop a **dashboard** for interactive exploration of the largest US companies dataset.  

