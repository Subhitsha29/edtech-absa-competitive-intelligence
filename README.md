# edtech-absa-competitive-intelligence
Aspect-Based Sentiment Analysis on 12,500 EdTech platform reviews

EdTech Competitive Intelligence: Aspect-Based Sentiment Analysis
An end-to-end NLP pipeline that transforms 12,500 Google Play Store reviews into a structured competitive intelligence matrix for five major EdTech platforms using transformer models and an interactive Power BI dashboard.

Problem
Overall app ratings hide why users like or dislike a platform. A single star rating combines content quality, instructor performance, pricing, user experience, certification, community, and customer support into one score. This makes it difficult for learners to choose the right platform and for EdTech companies to identify areas for improvement.
This project addresses that problem by analyzing 12,500 reviews across Coursera, Udemy, edX, LinkedIn Learning, and Pluralsight, classifying feedback into seven aspects, performing aspect-level sentiment analysis, and ranking improvement priorities for each platform.

Approach
Data
Collected 12,500 Google Play Store reviews using the google-play-scraper library
2,500 reviews per platform
Reviews balanced across the USA, India, UK, Australia, and Nigeria
Preprocessing
Cleaned and removed duplicate reviews with a 95.2% retention rate
Split reviews into 45,973 sentences using spaCy
Aspect Classification

Layer 1 :
Keyword-based rules classified 68.9% of sentences

Layer 2:
facebook/bart-large-mnli zero-shot classification assigned aspects to the remaining ambiguous sentences using a confidence threshold of 0.30

Sentiment Analysis:
Used cardiffnlp/twitter-roberta-base-sentiment-latest to score each sentence on a 0 to 10 scale
Selected RoBERTa over VADER because it better handles negation and contextual language in app reviews

Helpfulness Weighting:
Weighted detailed reviews more heavily using : 0.7 × normalized word count + 0.3 × normalized thumbs-up count

Must-Win Priority Analysis:
Designed a custom scoring model based on Importance × Gap from the market leader
Inspired by the Importance Performance Analysis framework by Martilla and James (1977)
Ranked the highest-priority improvement area for each platform


Built an interactive Power BI dashboard featuring:
KPI cards
Sentiment heatmap
Platform ranking
Aspect comparison
Platform-level slicer
Seven Aspects Analyzed
Content Quality
Instructor
Platform UX
Pricing
Support
Certification
Community

Key Findings:
1.edX emerged as the overall market leader with the highest average sentiment score and led in six of the seven aspects.
2.Platform UX was the weakest industry-wide aspect, with every platform scoring below the neutral benchmark of 5.0.
3.Coursera had the lowest Pricing score at 3.00, making pricing its most critical improvement area.
4.LinkedIn Learning recorded the lowest overall average sentiment of 2.90 and the lowest Instructor score of 2.50.
5.Community was the weakest aspect across all platforms, representing the biggest opportunity for competitive differentiation.

Tools and Libraries:
Python, Google Colab, NVIDIA T4 GPU, pandas, NumPy, spaCy, Hugging Face Transformers (BART and RoBERTa), Matplotlib, Plotly, WordCloud, Power BI Desktop


<img width="807" height="461" alt="Edtech Intelligence Dashboard" src="https://github.com/user-attachments/assets/a9ae7884-2f6d-4923-aefb-5acb97450350" />



Notebooks:
1. NB01_Data_Collection.ipynb — Scraping, cleaning, and sentence segmentation
2. NB02-Aspect Extraction.ipynb — Aspect classification (BART + keyword layer)
3. NB03_Sentiment_Scoring.ipynb — RoBERTa sentiment scoring
4. NB04_Competitive_Analysis.ipynb — Helpfulness weighting, Must-Win scoring, final aggregation
