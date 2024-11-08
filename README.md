### Python libraies for visualization

- Altair
- Seaborn
- Plotly
- Matplotlib
***************************************************************************
#### Altair

Common Chart Types
Altair provides many chart types such as:

`Bar Chart: .mark_bar()`  
`Line Chart: .mark_line()`  
`Scatter Plot: .mark_point()`  
`Area Chart: .mark_area()`  
`Histogram: .mark_bar()`  
`Box Plot: .mark_boxplot()`  

##### Encoding Types  
`x/y axis: x='column_name', y='column_name'`   
`Color: color='column_name'`    
`Size: size='column_name'`    
`Shape: shape='column_name'`    

##### Faceting with Row and Column Charts
```chart = alt.Chart(source).mark_point().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color='Color variable'
).facet(
    row='Row facet variable',
    column='Column facet variable'
).resolve_scale(
    x='independent',
    y='independent'
)
