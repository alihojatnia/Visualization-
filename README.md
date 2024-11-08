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

```
##### Interactive Legends
```
brush = alt.selection_point(fields=['Legend variable'], bind='legend')

chart = alt.Chart(source).mark_point().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color=alt.condition(brush, 'Legend variable', alt.value('lightgray')),
    opacity=alt.condition(brush, alt.value(1), alt.value(0.2))
).add_params(brush)


```
##### Layering and Concatenating Charts
```
chart1 = alt.Chart(source).mark_type().encode(
    x='X-axis variable',
    y='Y-axis variable'
)

chart2 = alt.Chart(source).mark_type().encode(
    x='X-axis variable',
    y='Y-axis variable'
)

alt.layer(chart1, chart2)

```

##### Using Selection to Filter Data Across Views
```
selection = alt.selection_point(encodings=['X-axis variable'])

chart1 = alt.Chart(source).mark_type().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color=alt.condition(selection, 'Color variable', alt.value('lightgray'))
).add_params(selection)

chart2 = alt.Chart(source).transform_filter(selection).mark_type().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color='Color variable'
)

alt.vconcat(chart1, chart2)

```

##### Heatmaps with Custom Tooltips
```
heatmap = alt.Chart(source).mark_rect().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color='Color variable'
).properties(width=300, height=300).encode(
    tooltip=['X-axis variable', 'Y-axis variable', 'Color variable']
)

```

##### Customizing Axis, Gridlines, and Titles
```
chart = alt.Chart(source).mark_point().encode(
    x=alt.X('X-axis variable', axis=alt.Axis(title='X-axis title', grid=False)),
    y=alt.Y('Y-axis variable', axis=alt.Axis(title='Y-axis title')),
    color='Color variable'
).properties(
    title='Chart Title',
    width=600,
    height=400
).configure_title(
    fontSize=20,
    anchor='start'
)

```

##### Dynamic Sizing with `alt.Size` and Encoding Conditionals
```
chart = alt.Chart(source).mark_circle().encode(
    x='X-axis variable',
    y='Y-axis variable',
    size=alt.Size('Size variable', scale=alt.Scale(range=[min, max])),
    color=alt.condition(
        alt.datum.Condition variable == 'value', 
        alt.value('Color 1'), 
        alt.value('Color 2')
    )
)
```

##### Parameter-based Dynamic Filtering
```
param = alt.param(value='default value')

chart = alt.Chart(source).transform_filter(
    alt.datum['Filtering variable'] > param
).mark_point().encode(
    x='X-axis variable',
    y='Y-axis variable',
    color='Color variable'
).add_params(param)

```

##### Using Window and Aggregate Transforms
```
chart = alt.Chart(source).transform_window(
    new_column='transform_expression',
    sort=[alt.SortField('Sort variable', order='descending')]
).mark_type().encode(
    x='X-axis variable',
    y='Y-axis variable'
).transform_filter(
    alt.datum.new_column < value
)

```

##### Using Images as Marks
```
chart = alt.Chart(source).mark_image(width=25, height=25).encode(
    x='X-axis variable',
    y='Y-axis variable',
    url=alt.value('image_url')
)

```
