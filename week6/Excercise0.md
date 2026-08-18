**Predicting Sales Revenue**
This is my own data set I have obtained so I can practice solving a regression problem. I intend to build three models (Linear Regression model using TensorFlow, a Dense Neural Network Model and XGBoost Decision Tree based model) and choose the best peforming model on test set.

Objective: Fit a regression model to predict sales revenue given the channel eg Web, WhatsApp, USSD, API.

Data: I have obtained training data set (csv) on sales revenue for e-tickets on various events for a period of close to 2 years. Each row of the data is a completed order containing order_id, order_created_at_date, channel_used (eg Web, WhatsApp, USSD, API), total_after_discount, event_start_date, event_end_date, event_category, event_category_name, payment_method.

Data Cleaning: Removed unnecessary fields ie fields that are irrelevant to the sales revenue.

Feature Engineering: Aggregate the rows to have weekly sales. I wrote a python script that grouped orders into weekly sales revenue, number of events in that week.

Here is where I am stack. Engineering the relevant features. I don't know which features I should construct so my model can learn to predict the sales amount given which features.

Brainstorming a solution:
I think given number of events (issue here is I would be predicting the number of events), period ie month and date, 

Taking a step back to the classic regression problem: Predicting the price of a house.
We need size of the house, number of bedrooms, location, price.

In my case week_number_in_a_month, month, channel, sales_revenue. This means I should extract the features the same way; week_num, month, channel, sales_renue. Here i am insisting on week_num because I can't do per month as my training examples m, is not large enough ie at approximately 2years I would less than 24 examples in my training set. 

I need to take a step back again and refine the regression problem I want to solve.
I need to answer these questions: 
1. Prediction unit:
2. Target variable:
3. Prediction time:
4. Information available at prediction time:
5. What I ultimately want the model to answer:


Two hours later... having done other things:
This is now my refined objective: Predict sales revenue per channel (Web, WhatsApp, USSD, API) for a particular month given the month, number_of_sports_events_scheduled_for_that_month, number_of_other_categories_of_events_for_that_month,
yhat = f(the month, number_of_sports_events_scheduled_for_that_month, number_of_other_categories_of_events_scheduled_for_that_month)
If m is small we can try week.

1. Prediction unit:
2. Target variable: Amount of predicted sales revenue per channel
3. Prediction time: An upcoming month.
4. Information available at prediction time: Number of sports and non sports events coming up in week number of the year, year, week number in the year
5. What I ultimately want the model to answer: How much are we going to sale per channel

This is now a multi-output regression model because yhat = [yWebaAmount,yUSSDAmount,...]
But standard XGBRegressor models a single target variable.

So I will refine the problem further so that it's a single output.

Refined objective: Predict sales revenue for channel c for a particular week of the year, number_of_sports_events_scheduled_for_that_week, number_of_other_categories_of_events_for_that_week,
yhatc = f(the week, number_of_sports_events_scheduled_for_that_week, number_of_other_categories_of_events_scheduled_for_that_week)

So I need my 4 training sets to include: week_number, num_of_sports_events_scheduled_for_that_week_num,num_of_non_sports_events_scheduled_for_that_week_num,channel_c_sales_revenue.

Will start with training set for ussd since this the one we care about the most.

SELECT 
    EXTRACT(YEAR FROM "createdAt") AS year_num,
    EXTRACT(WEEK FROM "createdAt") AS week_num, 
    ui, 
    COUNT(event)
    SUM("totalAfterDiscount") AS total_sales
FROM "KEventTicketsOrder"
WHERE ui = 'USSD' 
  AND status = 'Completed'
GROUP BY 
    EXTRACT(YEAR FROM "createdAt"), 
    EXTRACT(WEEK FROM "createdAt"), 
    ui
ORDER BY 
    year_num DESC, 
    week_num DESC;
