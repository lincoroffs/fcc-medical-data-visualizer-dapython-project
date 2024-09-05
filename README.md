# Medical Data Visualizer

In this project, you will visualize and make calculations from medical examination data using `matplotlib`, `seaborn`, and `pandas`. The dataset values were collected during medical examinations.

## Data description

The rows in the dataset represent patients and the columns represent information like body measurements, results from various blood tests, and lifestyle choices. You will use the dataset to explore the relationship between cardiac disease, body measurements, blood markers, and lifestyle choices.

File name: medical_examination.csv
<style>
  _ {
    text-shadow: none !important;
  }
  _, :after, :before {
    border: 0 solid #e5e7eb;
    box-sizing: border-box;
  }
  td, th {
    font-size: 1rem;
    font-weight: 400;
    margin: 0 0 1.2rem;
    color: #fff;
  }
  table {
    display: inline-block;
    overflow: auto;
    border-collapse: collapse;
    border-color: inherit;
    text-indent: 0;
    background-color: #303030;
  }
  table thead {
    border-color: inherit;
    display: table-header-group;
    vertical-align: middle;
  }
  table td, table th {
    border: 1px solid #666666 !important;
    padding: 6px 13px;
    text-align: center;
  }
  table th {
    font-weight: 700;
  }
  table tbody tr:nth-of-type(odd) {
    background-color: #404040;
  }
  code {
    white-space: break-spaces;
    background-color: #404040;
    border-radius: 0;
    color: #ccc;
    font-family: monospace;
    font-size: 90%;
    overflow-wrap: anywhere;
    padding: 1px 4px;
    font-feature-settings: normal;
    font-variation-settings: normal;
  }
  :not(pre)>code {
    border: 1px solid #999;
  }
  table code {
    white-space: nowrap;
  }
</style>
<table>
  <thead>
    <tr>
      <th>Feature</th>
      <th>Variable Type</th>
      <th>Variable</th>
      <th>Value Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Age</td>
      <td>Objective Feature</td>
      <td><code>age</code></td>
      <td>int (days)</td>
    </tr>
    <tr>
      <td>Height</td>
      <td>Objective Feature</td>
      <td><code>height</code></td>
      <td>int (cm)</td>
    </tr>
    <tr>
      <td>Weight</td>
      <td>Objective Feature</td>
      <td><code>weight</code></td>
      <td>float (kg)</td>
    </tr>
    <tr>
      <td>Gender</td>
      <td>Objective Feature</td>
      <td><code>gender</code></td>
      <td>categorical code</td>
    </tr>
    <tr>
      <td>Systolic blood pressure</td>
      <td>Examination Feature</td>
      <td><code>ap_hi</code></td>
      <td>int</td>
    </tr>
    <tr>
      <td>Diastolic blood pressure</td>
      <td>Examination Feature</td>
      <td><code>ap_lo</code></td>
      <td>int</td>
    </tr>
    <tr>
      <td>Cholesterol</td>
      <td>Examination Feature</td>
      <td><code>cholesterol</code></td>
      <td>1: normal, 2: above normal, 3: well above normal</td>
    </tr>
    <tr>
      <td>Glucose</td>
      <td>Examination Feature</td>
      <td><code>gluc</code></td>
      <td>1: normal, 2: above normal, 3: well above normal</td>
    </tr>
    <tr>
      <td>Smoking</td>
      <td>Subjective Feature</td>
      <td><code>smoke</code></td>
      <td>binary</td>
    </tr>
    <tr>
      <td>Alcohol intake</td>
      <td>Subjective Feature</td>
      <td><code>alco</code></td>
      <td>binary</td>
    </tr>
    <tr>
      <td>Physical activity</td>
      <td>Subjective Feature</td>
      <td><code>active</code></td>
      <td>binary</td>
    </tr>
    <tr>
      <td>Presence or absence of cardiovascular disease</td>
      <td>Target Variable</td>
      <td><code>cardio</code></td>
      <td>binary</td>
    </tr>
  </tbody>
</table>

## Tasks
Create a chart similar to `examples/Figure_1.png`, where we show the counts of good and bad outcomes for the `cholesterol`, `gluc`, `alco`, `active`, and `smoke` variables for patients with `cardio=1` and `cardio=0` in different panels.

Use the data to complete the following tasks in `medical_data_visualizer.py`:

- Add an `overweight` column to the data. To determine if a person is overweight, first calculate their BMI by dividing their weight in kilograms by the square of their height in meters. If that value is > 25 then the person is overweight. Use the value `0` for NOT overweight and the value `1` for overweight.
- Normalize the data by making `0` always good and `1` always bad. If the value of `cholesterol` or `gluc` is `1`, make the value `0`. If the value is more than `1`, make the value `1`.
- Convert the data into long format and create a chart that shows the value counts of the categorical features using `seaborn`'s `catplot()`. The dataset should be split by `Cardio` so there is one chart for each `cardio` value. The chart should look like `examples/Figure_1.png`.
- Clean the data. Filter out the following patient segments that represent incorrect data:
  - diastolic pressure is higher than systolic (Keep the correct data with `(df['ap_lo'] <= df['ap_hi'])`)
  - height is less than the 2.5th percentile (Keep the correct data with `(df['height'] >= df['height'].quantile(0.025))`)
  - height is more than the 97.5th percentile
  - weight is less than the 2.5th percentile
  - weight is more than the 97.5th percentile
- Create a correlation matrix using the dataset. Plot the correlation matrix using `seaborn`'s `heatmap()`. Mask the upper triangle. The chart should look like `examples/Figure_2.png`.

Any time a variable is set to `None`, make sure to set it to the correct code.

Unit tests are written for you under `test_module.py`.

## Instructions
By each number in the `medical_data_visualizer.py` file, add the code from the associated instruction number below.

1. Import the data from `medical_examination.csv` and assign it to the `df` variable
2. Create the `overweight` column in the `df` variable
3. Normalize data by making `0` always good and `1` always bad. If the value of `cholesterol` or `gluc` is `1`, set the value to `0`. If the value is more than `1`, set the value to `1`.
4. Draw the Categorical Plot in the `draw_cat_plot` function
5. Create a DataFrame for the cat plot using `pd.melt` with values from `cholesterol`, `gluc`, `smoke`, `alco`, `active`, and `overweight` in the `df_cat` variable.
6. Group and reformat the data in `df_cat` to split it by `cardio`. Show the counts of each feature. You will have to rename one of the columns for the `catplot` to work correctly.
7. Convert the data into `long` format and create a chart that shows the value counts of the categorical features using the following method provided by the seaborn library import: `sns.catplot()`
8. Get the figure for the output and store it in the `fig` variable
9. Do not modify the next two lines
10. Draw the Heat Map in the `draw_heat_map` function
11. Clean the data in the `df_heat` variable by filtering out the following patient segments that represent incorrect data:
  - height is less than the 2.5th percentile (Keep the correct data with `(df['height'] >= df['height'].quantile(0.025))`)
  - height is more than the 97.5th percentile
  - weight is less than the 2.5th percentile
  - weight is more than the 97.5th percentile
12. Calculate the correlation matrix and store it in the `corr` variable
13. Generate a mask for the upper triangle and store it in the `mask` variable
14. Set up the `matplotlib` figure
15. Plot the correlation matrix using the method provided by the `seaborn` library import: `sns.heatmap()`
16. Do not modify the next two lines

## Development
Write your code in `medical_data_visualizer.py`. For development, you can use `main.py` to test your code.