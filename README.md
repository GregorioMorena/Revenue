# Revenue
## Analysis and an attempt to predict future sales.

We were asked to help a small restaurant, that wanted to implement ML models to predict the future sales.

This restaurant only sells Argentine empanadas. They were facing a serious problem with predicting sales since the empanadas must be pre-cooked to be served timely. This means that if they underestimated sales, they won't be able to serve their clients and on the other hand, if they overestimated sales, they will waste empanadas.

We start this consulting with just their daily sales since its opening in October 2020. Could we develop a predictive model for them? No, and nobody could. But we tried to help them anyway.

Our analysis started looking at the sales behaviour. We noticed that the sales were very volatile in the firsts month after the opening, and that their sales decrease in the lasts months. They explained us that the access to the restaurant was restringed due to roadworks.

### <p align="center"> Total sales by dates </p>
<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/allsales.png">
</p>

So we decided to keep only the first four month of 2021, to try to understand the sales behaviour in normal circunstances.

### <p align="center"> Sales in normal circunstances </p> 
<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/normalsales.png">
</p>

Our next issue was having no features for our model but the date. What kind of information could we extract from a date? We had to figure it out before making any exploratory data analysis.

We started with three obvious approaches: the day of the month, the day of the week and the week of the month.

### <p align="center"> Our very first features </p> 
<p align="center">
  <img width="920" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/primarfeatures.png">
</p>

And that was a great begining! We could notice how this features affected our target (the sales). But we had to try to get more information from this dataset. In one step of our EDA we get this plot:

### <p align="center"> A heatmap with the avarage sales </p> 
<p align="center">
  <img width="920" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/heatmap.png">
</p>

We saw that weekdays (4 is Friday and 5 is Saturday) joined with the week of the month combined had a strong correlation with the average sales. So we create a feature combining the weekday and the week of the month.

```
df['hot_dates'] = (df['weekday'] == 4) | (df['weekday'] == 5)
df['hot_dates'] = df['hot_dates'] * (df['week'] + df['weekday']) + (df['week'] == 0)
```

We also created some features with the average sales for the current weekday and the current week of month. The final features correlation matrix was this:

<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/corr.png">
</p>

## Conclusion

After trying (at the request of the customer) finding a predictive model, we were able only to deliver a simple insight about the sales behaviour across the dates.

Developing a predicitive model requieres more data for sure, but now this small restaurant counts at least on a primary analysis on which to plan its production.

### <p align="center"> Linear Regression error </p> 
<p align="center">
  <img width="460" height="300" src="https://raw.githubusercontent.com/GregorioMorena/Revenue/main/linreg.png">
</p>
