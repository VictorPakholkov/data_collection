# Home Assignment 1 conclusions 

I do not understand how should final thoughts and conclusions look like for the task to tell the truth:)

The general work proccess was fun and enlightening. The topic was proposed by ChatGPT, as I have little idea of what I would like to collect.

The search for an open dataset involved a examination of available resources such as Kaggle, Harvard Data Hub, and governmental agencies (majority US and EU ones are banning Russian IPs, lol). The choice of the "Air Quality Annual Summary" dataset from the Environmental Protection Agency (EPA) was justified by avaliability on Kaggle, relevance to the theme and useful description.

Usingg the Air Quality System (AQS) API for data enhancement added a new dimension to the dataset. The API offered a structured means to retrieve additional observations beyond the original dataset's temporal scope. This step underscored the significance of incorporating real-time or recent data to keep analyses relevant and reflective of current conditions.

EDA uncovered some general patterns and trends within the resulting dataset.At the same time, many things were very strange - e.g. strange peak outliers, like 1990 outlier of benzene which might have come from different sources, but was smoothed by log transformation to make sense at all. Understanding the distribution of air quality metrics, temporal trends, and spatial variations provided some modest insights. The use of visualizations facilitated the understanding of complex patterns (actually were the only means of understanding for such data).

The dataset's richness and diversity open avenues for machine learning applications. Tasks such as regression for predicting air quality metrics, classification for categorizing air quality levels, time-series analysis, anomaly detection, and spatial modeling emerge as potential ML use cases. The dataset's temporal and spatial dimensions provide ample opportunities for developing models that capture the complexity of air quality dynamics.

More details on each point are within .ipynb file 'API_aqs'. 
Thanks!
