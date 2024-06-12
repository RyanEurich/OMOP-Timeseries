# Time Series Forecast for hospital occupation by patients

## Data | Context
This data represents the total number of patients in each hospital section at each time. It is broken down by year, month, day, and hour. It was pulled from a modified UCI Health report from their medical center in Orange, mapped to the standard OMOP data model. The years are shifted but the data examined was over a 10 year timeframe. There were no null or missing time values but other id's and non time information were dropped.

I did the initial exploration and analysis in Azure Data Studio in mssql to examine disease trends among different racial and ethnic groups. The visit_detail, visit_occurrence, and assignment were queried into a single table and exported to a csv. From there, they were one hot encoded into a year, month, day, hour format in a local jupyter notebook file before uploading that to deep note. 

## Analysis | Results
We used 3 main models to examine patient inflow and occupation. These were the Facebook Prophet model, A RNN, and a Transformer. These all only used time and no other factors. Weekends, and Holidays were not encoded into the NN models. We can see that December has many visits along with Monday's.

### Facebook Prophet
The first pure time series model we looked at was facebook prophet, an industry staple.We got decent results but the level of fine tuning required to capture all the fluctuations in seasonality and other factors proved to be quite finicky. ARMIA models were also considered but I assumed they would do no better than prophet  

### MLP Neural Network 
The next model we tried was a feed forward multi-layer MLP. These are generally known to be good at time and the context of it. We got 86% R^2 during our test which was quite good considering our prior attempts. We settled on 3 layers after tuning some parameters. The time data was scaled and no other factors were included. 

### Tranformer Model
Our last attempt at a model was using a transformer architecture, known as the cutting-edge and great with attention and sequences, this was our best bet. We eventually got up to 87% accuracy, not much better than our MLP but still a great result.  The underlying details were encoder decoder, seq to vector output, predicting each value at a time. With further tuning and adding other time features this could easily get above 90%

## Conclusion | Next Steps
This was forecasted a hospital wide level. We could break this down by section or ward to get more granular results. Furthermore we could incorporate other tables such as condition to analyze the conditions that people are admitted to the most or the times where the most deaths occur. Adding in other features to make multivariate models may lead to even more accurate results.
