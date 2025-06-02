# Text Analysis and Sentiment Scoring Project

## Overview
This project involves web scraping, text preprocessing, and sentiment analysis of articles from a provided list of URLs. The goal is to extract article titles and content, clean the text, and compute various textual and sentiment metrics such as positive/negative scores, polarity, subjectivity, and readability indices. The processed data is then saved into an Excel file for further analysis.

## Project Description
The project processes a dataset (`Input.xlsx`) containing URLs and their corresponding IDs. It performs the following tasks:
1. **Web Scraping**: Extracts article titles and content from the given URLs using the `requests` and `BeautifulSoup` libraries.
2. **Text Cleaning**: Removes unnecessary characters, stopwords, and applies lemmatization to standardize the text.
3. **Sentiment Analysis**: Calculates positive and negative scores using predefined dictionaries of positive and negative words.
4. **Text Metrics**: Computes metrics like polarity score, subjectivity score, average sentence length, percentage of complex words, Fog Index, word count, syllable count per word, personal pronoun count, and average word length.
5. **Output**: Saves the results to an Excel file (`output_data.xlsx`) with all computed metrics.

## Dependencies
The project relies on the following Python libraries:
- `requests`: For making HTTP requests to fetch web pages.
- `beautifulsoup4`: For parsing HTML content and extracting relevant data.
- `pandas`: For handling data in tabular form and Excel file operations.
- `numpy`: For handling missing values and numerical operations.
- `nltk`: For natural language processing tasks such as tokenization, stopword removal, and lemmatization.
- `re`: For regular expression-based text cleaning.
- `glob` and `os`: For file handling operations.
- `openpyxl`: For reading and writing Excel files.

## Input Files
- **Input.xlsx**: Contains two columns: `URL_ID` (unique identifier for each URL) and `URL` (the web address of the article to be scraped).
- **positive-words.txt**: A text file containing a list of positive words for sentiment scoring.
- **negative-words.txt**: A text file containing a list of negative words for sentiment scoring.
- **stopwords/**: A directory containing text files with stopwords to be removed during text cleaning.

## Output
- **output_data.xlsx**: The output Excel file containing the following columns:
  - `URL_ID`: Unique identifier for each URL.
  - `URL`: The web address of the article.
  - `POSITIVE SCORE`: Count of positive words in the article.
  - `NEGATIVE SCORE`: Count of negative words in the article.
  - `POLARITY SCORE`: Calculated as `(Positive Score - Negative Score) / (Positive Score + Negative Score + 0.000001)`.
  - `SUBJECTIVITY SCORE`: Calculated as `(Positive Score + Negative Score) / (Total Words + 0.000001)`.
  - `AVG SENTENCE LENGTH`: Average number of words per sentence.
  - `PERCENTAGE OF COMPLEX WORDS`: Percentage of words with more than two syllables.
  - `FOG INDEX`: Readability metric calculated as `0.4 * (Average Sentence Length + Percentage of Complex Words)`.
  - `AVG NUMBER OF WORDS PER SENTENCE`: Same as average sentence length.
  - `COMPLEX WORD COUNT`: Count of words with more than two syllables.
  - `WORD COUNT`: Total number of words in the article.
  - `SYLLABLE PER WORD`: Average number of syllables per word.
  - `PERSONAL PRONOUNS`: Count of personal pronouns in the article.
  - `AVG WORD LENGTH`: Average length of words in characters.

## Workflow
1. **Data Loading**: Read the input Excel file (`Input.xlsx`) containing URLs.
2. **Web Scraping**: For each URL, fetch the webpage, parse it using BeautifulSoup, and extract the article title and content.
3. **Text Cleaning**:
   - Remove special characters and extra spaces using regular expressions.
   - Tokenize the text and remove stopwords from a provided stopwords directory.
   - Apply lemmatization to standardize words.
4. **Sentiment and Text Analysis**:
   - Calculate positive and negative scores using word dictionaries.
   - Compute polarity and subjectivity scores.
   - Calculate readability and complexity metrics such as Fog Index, average sentence length, and syllable counts.
5. **Data Processing**:
   - Handle missing data by dropping rows where articles could not be scraped.
   - Merge the computed metrics into a new DataFrame.
6. **Output**: Save the final DataFrame with all metrics to `output_data.xlsx`.

## Error Handling
- The script handles cases where article content or titles are missing by returning `NaN` and subsequently dropping such rows.
- It accounts for edge cases like empty texts or zero sentences/words during metric calculations by adding a small constant (`0.000001`) to denominators.

## Usage
To run the project:
1. Ensure all dependencies are installed (`pip install requests beautifulsoup4 pandas numpy nltk openpyxl`).
2. Download the required NLTK data (`stopwords`, `punkt`, `wordnet`).
3. Place the input files (`Input.xlsx`, `positive-words.txt`, `negative-words.txt`, and the `stopwords/` directory) in the project directory.
4. Run the script to generate `output_data.xlsx`.

## Notes
- The project assumes that the stopwords directory contains text files with stopwords, and the positive/negative word files are properly formatted.
- Some URLs may not have accessible content due to website structure changes, resulting in `NaN` values that are dropped in the final output.
- The sentiment dictionaries (`positive-words.txt`, `negative-words.txt`) should be comprehensive for accurate scoring.
- The readability metrics (e.g., Fog Index) are calculated based on standard formulas but may vary slightly depending on the tokenization and syllable counting logic.

## Future Improvements
- Enhance web scraping to handle dynamic websites or JavaScript-rendered content using tools like `selenium`.
- Expand the sentiment dictionaries to include more context-specific words.
- Add support for additional readability metrics or sentiment analysis techniques (e.g., using machine learning models).
- Improve error handling for network issues or malformed web pages.
