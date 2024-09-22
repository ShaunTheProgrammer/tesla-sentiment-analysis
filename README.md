# Tesla Social Media Sentiment Analysis

## Project Overview

This project analyzes social media sentiment surrounding Tesla on Reddit to track brand reputation and consumer trends. By leveraging Natural Language Processing (NLP) techniques, the goal is to provide Tesla with insights on how they are perceived online and identify areas of improvement.

### Objective

The objective of this project is to:
- **Analyze sentiment** of Reddit posts and comments related to Tesla.
- Identify trends in **positive, negative, and neutral** sentiment.
- Provide **actionable insights** for Tesla's marketing and public relations teams.

---

### Data Collection

Data collection was performed using the Reddit API (PRAW) to scrape posts and comments mentioning Tesla. Here is a breakdown of the process:

1. **API Setup**:
   - To start, I created a Reddit Developer account and registered an application to gain access to the Reddit API using the `PRAW` (Python Reddit API Wrapper) library.
   - The API allowed me to scrape data from subreddits that mentioned Tesla or discussed topics related to electric vehicles, autonomous cars, or the tech industry in general.
   
2. **Post Criteria**:
   - I scraped posts that mentioned “Tesla” in either the title or selftext (the body of the post) to capture a broad range of opinions.
   - Both the post titles and body (selftext) were collected to analyze sentiment from the initial post content and the deeper discussion in the body.

3. **Comment Collection**:
   - For each post, I also collected the top comments as they represent user engagement and reactions.
   - This way, I captured both the initial sentiment of the post and the reactionary sentiment from the community.
   
4. **Fields Collected**:
   - Post title, post selftext (if any), comments (top-level comments), date of the post, and sentiment scores from each of the text sections.
   - Over 200 posts and their associated comments were collected, totaling hundreds of data points for analysis.

---

### Data Cleaning

After gathering the raw data, significant preprocessing steps were necessary to prepare it for sentiment analysis. Here are the data cleaning tasks performed:

1. **Handling Missing Data**:
   - Some Reddit posts may have had empty selftexts or no comments at all. I handled these by imputing or marking missing values as necessary.
   - Posts with no relevant content (i.e., no selftext or comments) were dropped from the dataset.

2. **Removing Duplicates**:
   - I removed any duplicate posts that may have been scraped multiple times due to different API calls.
   - Ensured that each unique post and its associated comments were retained.

3. **Text Preprocessing**:
   - **Lowercasing**: Converted all text to lowercase to standardize the dataset.
   - **Removing Special Characters**: Stripped special characters like hashtags, URLs, and symbols to focus purely on the textual sentiment.
   - **Stopwords Removal**: I removed common English stopwords like "the", "is", "in", "and", etc., as they don’t contribute to sentiment but add noise.
   - **Tokenization**: Split text into individual words or tokens, which is necessary for sentiment analysis algorithms.

4. **Handling Outliers**:
   - Titles or comments that were overly short or too long were handled appropriately (either removed or truncated) to ensure they wouldn't skew the analysis.

---

### Sentiment Analysis

The core of the project was the sentiment analysis of Tesla-related posts and comments. Here’s a breakdown of the sentiment analysis process:

1. **VADER Sentiment Analysis**:
   - I used the **VADER (Valence Aware Dictionary and Sentiment Reasoner)** sentiment analysis tool, which is highly effective for social media text due to its ability to handle slang, emojis, and punctuation.
   - VADER returns a **compound sentiment score** for each text input, which ranges from -1 (most negative) to 1 (most positive), and also provides granular scores for positivity, negativity, and neutrality.

2. **Sentiment Scores**:
   - For each post and comment, I calculated a compound sentiment score using VADER. Here’s how I categorized the sentiment:
     - **Positive Sentiment**: Compound score > 0.05
     - **Neutral Sentiment**: Compound score between -0.05 and 0.05
     - **Negative Sentiment**: Compound score < -0.05
   - This method allowed me to classify each post and comment into **positive**, **neutral**, or **negative** sentiment categories.

3. **Title, Selftext, and Comment Sentiment**:
   - Each post was broken down into its individual components: **title**, **selftext**, and **comments**.
   - I calculated separate sentiment scores for each of these components, allowing for a detailed comparison between how Tesla is initially presented (through post titles) and how users react (through comments).
   
4. **Sentiment Category Classification**:
   - I categorized each title, selftext, and comment sentiment into **positive**, **neutral**, and **negative** sentiment based on the VADER score to provide clear insights into how Tesla is perceived.

5. **Sentiment Distribution and Trends**:
   - By analyzing the sentiment scores over time, I explored how discussions about Tesla evolved and whether posts started negatively but transitioned to positive in the comments section.
   - I created visualizations to show the distribution of sentiment scores across posts and comments, identifying dominant trends in user discussions.

---

### Visualizations

Here are some key visualizations generated during the analysis:

- **Box Plots** of Title vs. Comment Sentiment: Show the range of sentiments for post titles and corresponding comments.
- **Scatter Plot** of Title Sentiment vs. Comment Sentiment: Displays the relationship between the initial post title and community response.
- **Distribution of Sentiment Scores** for Titles and Comments: Highlights how frequently Tesla-related discussions are positive, neutral, or negative.
- **Sentiment Categories** (Positive, Neutral, Negative) for Titles and Comments: Showcases the sentiment categories based on VADER classification.

![image](https://github.com/user-attachments/assets/3b5b6f6c-855f-4a3c-a029-0dba33d99d09)
![image](https://github.com/user-attachments/assets/09410fa5-8e77-4ab1-8171-c8b3a7fab3fd)
![image](https://github.com/user-attachments/assets/9b59a512-afdc-403f-bba0-7ad7f3fe4134)
![image](https://github.com/user-attachments/assets/1947c36e-88ed-4242-a1a8-ff1c93983adf)

---

### Key Insights

#### 1. Overall Sentiment
- **Selftext Sentiment**: Predominantly negative (-0.296), reflecting criticism or concerns in discussions.
- **Title Sentiment**: Ranges from positive to neutral to negative, without a clear dominant polarity.
- **Comment Sentiment**: Mostly positive (0.7–0.9), indicating strong community support for Tesla despite critical posts.

#### 2. Misalignment Between Title and Comment Sentiment
- Negative post titles often attract positive comments, suggesting a loyal community ready to defend the brand.

#### 3. Positive Sentiment in Comments
- Even posts with neutral or negative titles generally have positive comments, indicating positive user engagement around Tesla.

---
### Potential Business Impacts

#### 1. **Reputation Management**:

Tesla should focus on monitoring negative post titles and selftexts, but they can rely on the strong positive community engagement in the comments. A proactive response strategy, particularly for high-engagement negative posts, could help convert neutral audiences into positive advocates, further amplifying their supportive community.

#### 2. **Community Engagement Strategy**:

Tesla can leverage the insight that even critical discussions frequently result in positive interactions in the comments. This suggests the company can address negative conversations head-on, knowing that their supporters will often come to Tesla’s defense.

#### 3. **Product Feedback and Improvement**:

Tesla should track and analyze topics with consistently negative sentiment in post titles or selftexts to identify potential product or service issues. Addressing these concerns in future updates or customer service efforts can prevent negative sentiment from escalating and could convert detractors into advocates.

---

### Actionable Recommendations

- **Reputation Management**: Tesla should engage with high-engagement negative posts and respond proactively.
- **Community Engagement**: Leverage the positive community sentiment by encouraging more interaction and discussions.
- **Monitor Negative Trends**: Track frequent negative themes and address them through product updates or PR strategies.

---

### Folder Structure

```bash
tesla-sentiment-analysis/
│
├── data/
│   ├── raw_reddit_data.csv          # Raw data collected from Reddit API
│   ├── final_sentiment_data.csv     # Final dataset with sentiment analysis
│
├── notebooks/
│   └── SocialMediaProject.ipynb     # Jupyter notebook with analysis code
│
├── README.md                        # Project overview (this file)
└── LICENSE.md                       # License file
