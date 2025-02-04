# Data Preparation and Optimization for Product Marketing
## Table of Contents
1. [Introduction](#introduction)
2. [Tools and Libraries Used](#tools-and-libraries-used)
3. [Objective](#objective)
4. [Dataset Overview](#dataset-overview)
5. [Approach and Methodology](#approach-and-methodology)
    - [1. Data Cleaning and Standardization](#1-data-cleaning-and-standardization)
    - [2. Removing Redundant Phrases](#2-removing-redundant-phrases)
    - [3. Extracting Relevant Product Details](#3-extracting-relevant-product-details)
    - [4. Generating Product Descriptions](#4-generating-product-descriptions)
    - [5. Handling Missing Values](#5-handling-missing-values)
6. [Conclusion](#conclusion)

## Introduction
The dataset under review contains 3,487 rows and 7 columns, each detailing various product attributes. It is critical to ensure that the data is not only accurate but also optimized for search engine visibility and user readability. To achieve this, a combination of data cleaning and natural language processing (NLP) techniques has been employed. The purpose of this report is to outline the methods used to prepare the dataset for marketing analysis, which includes data standardization, handling missing values, and the creation of a new feature aimed at improving product descriptions and titles.

By utilizing tools like spaCy for text processing, pandas for data manipulation, and regular expressions for targeted cleaning, we aimed to enhance the dataset's overall quality while optimizing product titles for improved SEO.

## Tools and Libraries Used
- **spaCy**: A robust NLP library used to tokenize and process product titles, extracting meaningful elements such as product names, brands, and sizes.
- **pandas**: A data manipulation library that facilitated the cleaning and standardization of data in tabular form.
- **re (Regular Expressions)**: Employed to identify and remove redundant phrases from product titles, as well as extract size-related details.

## Objective
The objective of this analysis was to prepare the raw marketing dataset for further analysis by addressing data quality issues and creating a new feature, `short_title`, aimed at improving product visibility through better SEO practices. Key tasks included resolving missing values, identifying duplicates, standardizing formats, and generating concise product titles for increased marketing impact.

## Dataset Overview
| Columns            | Description                                                                 | Data Type       | Data Classification |
|--------------------|-----------------------------------------------------------------------------|-----------------|---------------------|
| product_id         | A unique identifier for each product                                         | Integer         | Nominal             |
| title              | The title or name of the product                                             | String/text     | Nominal             |
| bullet_points      | Key features or attributes of the product listed as bullet points            | String/text     | Nominal             |
| description        | A detailed description of the product, providing information about features, specifications, etc | String/text     | Nominal             |
| product_type_id    | A unique identifier for the type or category of the product                  | Float/Decimal   | Ordinal             |
| product_length     | The length of the product, typically used for packaging or shipping purposes | Float/Decimal   | Ratio               |

## Approach and Methodology

### 1. Data Cleaning and Standardization
I began by addressing the most immediate quality issues: duplicates and inconsistent column names. This process included:
- **Standardizing column names**: Ensuring all column names were consistent and easy to understand.
- **Removing duplicates**: A total of 523 duplicate entries were identified and removed, leaving a clean dataset ready for further processing.

_Image 1: Showing results before and after removing duplicates and standardizing the columns_

### 2. Removing Redundant Phrases
To streamline product titles, we targeted common phrases that did not add value to the product description. A predefined list of phrases such as "features", "best", "color options", and "new" was compiled. These phrases were frequently found in product titles but contributed little to overall clarity or SEO performance.
- **Regular expressions** were used to match and remove these redundant phrases.
- **Extra spaces** were eliminated using a secondary regular expression to ensure the cleaned product titles were formatted correctly.

### 3. Extracting Relevant Product Details

#### Product Name and Brand
Using the spaCy NLP model, we focused on extracting key product details. The following steps were taken:
- **Product Name Extraction**: Proper nouns (e.g., names of products or brands) were identified from the title. The first three relevant words were selected to form the product name, ensuring titles remained concise.
- **Brand Identification**: If a brand name was detected in the first few proper nouns, it was recorded separately for further analysis.

#### Product Size
To extract product size information, regular expressions were employed. We created a pattern to detect measurements such as "inch", "cm", "mm", and "pcs" from the title.
- **Size Extraction**: The `findall()` method was used to search for size-related information. These sizes were then stored in a list (`size_chart`) for use in generating more detailed product descriptions.

### 4. Generating Product Descriptions
After cleaning the data and extracting key details, new product descriptions were generated. The detailed product description incorporated the cleaned title, product name, and size information, providing a more structured and informative overview of each product. A short title was also generated using the product name and size information, designed for SEO optimization, making it easier for potential customers to find the product online.

_Image 2: Showing the new cleaned column ‘short title’ and how it compares with the original ‘title’ column_

### 5. Handling Missing Values
Missing values were addressed systematically:
- **Detecting Missing Data**: I used the `isnull().sum()` function to identify missing values across all columns. This allowed us to detect and address gaps in the data that could affect further analysis.
- **Imputation Strategy**: For the `bullet_points` column, if values were missing, they were replaced with corresponding entries from the `description` column. This ensured that product listings had comprehensive information even when specific bullet points were not available. The rationale behind this approach was that a detailed description could act as a suitable substitute for missing bullet points, maintaining the completeness of the dataset.

## Conclusion
This analysis enhanced the quality and usability of the dataset by implementing data cleaning procedures, extracting relevant product details, and generating SEO-optimized short titles. The prepared dataset is now well-structured for further marketing analysis, offering valuable insights into product attributes and improving overall data readability for customers and stakeholders alike.
