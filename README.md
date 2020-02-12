# Chicago Airbnb Analysis

## Purpose
This project analyzes Chicago Airbnb data to optimize a West Loop Airbnb listing. Overview reflected in a Medium
blog post (here: https://medium.com/@molly.king32/become-a-chicagoan-entrepreneur-611c6a15e4e7).

## Project Structure
This project follows the CRISP-DM process structure:
1.  Business Understanding
  -Airbnb's Chicago dataset was used for this project.  Only the listings data was used.
  -This data was used to answer the following questions:
    1.  What is the Airbnb rental market like in Chicago?
    2.  What is the Airbnb rental market like in the West Town neighborhood?
    3.  What is the Airbnb rental market like in the neighborhoods that compete with West Town?
2.  Data Understanding
  -Airbnb's Chicago dataset was used for this project.  Only the listings data was used.
  -This data is current as of November 2019.
  -Each row represents one property booked on Airbnb's website.  There can be multiple rows per host if hosts manage multiple properties.
  -This site was used to visualize the dataset provided (http://insideairbnb.com/chicago/?neighbourhood=&filterEntireHomes=false&filterHighlyAvailable=false&filterRecentReviews=false&filterMultiListings=false).
3.  Data Preparation
  -Listings data is read into the notebook.
  -Any columns where all records are null are dropped (only impacts one column, neighbourhood_group).  They provide no new data so it does not make sense to retain them.
  -Any remaining missing values are treated.  'Reviews_per_month' NA values are changed to zeros, as there are no reviews yet for these listings.  Any 'last_review' columns missing a date are subbed with '1900-01-01' to flag they've never received a review.  It makes sense to treat these issues as the majority of values are present, so we would retain more value by fixing rathern than dropping.
  -A suburbs column is created using 'neighbourhoods'.  If the listing is in a suburban neighborhood, it is given a value of "1", representing true.  Otherwise it is tagged as "0" representing false, it is a city listing.  This allows us to sense check the data, as most listings would likely be in the city rather than further out.  It also provides more insight into the true split and behavior of the market.
  -Neighborhoods with very small counts are then tagged to "Other" to minimize the noise in the dataset.  Any neighborhoods with less than 20 bookings are combined into the "Other" category.  
  -Dummy variable are then created for all categorical variables.  This makes it easier to visualize behavior within each neighborhood using histograms.  It also gives us flexibilty if we need to model downthe road because we already have all our dummy variables included in our dataset.
  -Feature engineering is then utilized again to create the following variables:
    -days_since_last_review: number of days elapsed since the property was last reviewed
    -pct_time_available: % of the year each listing is available to be booked
    -min_stay_cost: multiplies the price by the minimum night stay required by the host to get the minimum cost to book each listing
  -Extremes and outliers are then replaced with medians (any values less than the 25th percentile or greater than the 75th percentile).  Medians were used because they are less easily influenced by extreme values than means.  This step was also taken to get better understanding of the majority of records.  Histogram shapes and true distributions can be distorted by a few extremely high values, such as Airbnb listings with a high price.
  -Neighborhood specific datasets are then created to support generating insights (West Town only, River North only, etc.)
  -Analysis is conducted to answer the above questions in step 1.
4.  Modeling
  -No modeling was used in this project
5. Evaluation
  -The following mental sense checks were applied:
    -Are these prices reasonable?  Do they make sense?
    -Does this story / these insights make sense as a holistic picture about the Airbnb market in Chicago?
    -Do prices and neighborhood popularity make sense given what is already known about Chicago (South Side not a popular destination, lots to do in Near North, etc.)?
    -Do all values make sense post-outlier replacement?  Checked using before and after histograms.
 6.  Deployment
  -Commit to Github
  -Publish on Medium
