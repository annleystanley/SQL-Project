# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals

My main goal from this project, is to find meaningful relationships within the provided ecommerce dataset. I hope to show the relationship between specific geographical locations and their purchasing habits, as well as the effects of price, restocking times, and product types, may have on purchasing habits.

## Process

### Step 1)

My first step was to familiarize myself with the data, this took a while since there was an overwhelming amount of it. I ran several queries checking values from one table against another.

### Step 2)

Following that, it was time to clean data based on the questions being asked. I focused on location data, products, and revenue. This meant altering/deleting rows with null values, deleting outliers, and filling in data where I could.

### Step 3)

As I worked through answering questions, I realised that cleaning was an ongoing process. I frequently found myself realising more changes would need to be made.

For the sake of my own sanity, I made several extra tables that included ONLY cleaned location data, and ONLY cleaned transaction & product data. They had fewer values overall, but they had more quantifiable data that could be used.

### Step 4)

Using a pared down amount of data made results easier and clearer to see, but also made me realise that it made more sense to look at things on a larger scale due to the limited verifiable location data. For my own questions, I focused on broader questions with more general answers.

## Results

I had a hard time finding meaningful results from this data. Since a large amount of it was missing, it feels like my results are not completely accurate.

I did find that apparel and electronics were very popular categories, and that overall, people are much more likely to window-shop than they are to actually make a purchase. Products that are restocked quickly, also tend to sell more (most likely do to a higher availability).

One interesting result, was finding that there is a certain "sweet" spot for a product price. After an analysis of product prices, and sales, I discovered that people are most likely to make purchases that are in between the mean price of $33 and the median of $18.99.

## Challenges 

I faced many technical, as well as personal challenges while doing this project.
Despite having a computer with 8gb of ram, one of the datasets was mostly unworkable for me, and frequently caused crashes.  I ended up not using it, which makes me worried I may have lost out on some valuable data.

Data cleaning was also a challenge. Knowing what to prioritize when it came to cleaning, was very difficult. I wanted to complete the project on time, but did not want to feel like I was sacrificing quality for the sake of time.

I also faced the challenge of wanting to make sure I had the SQL knowledge to complete the project, while also needing help in several areas.  There is a fine line between asking someone for help on code, and copying what someone else did, and I wanted to try to reach conclusions on my own as much as I could.

## Future Goals

If I had more time, I would spend more time planning my process, especially when it comes to cleaning. My cleaning process felt very rushed and I feel as though there are several key factors that I missed. I would have spent more time assigning product categories to items without any, and looking for better and more efficient ways to utilize my time.

I also would have documented my work better, as I noticed parts of my process missing (i.e. my code to get a quantity_ordered table (which was assuming that the quantity ordered was totaltransactionrevenue/productprice)). Next time, I will document more thoroughly as I go through the process.