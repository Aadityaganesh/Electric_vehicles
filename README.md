# Performing EDA on Electric Vehicle Data

This repository contains the code and analysis I have performed. The project focuses on Exploratory Data Analysis (EDA) of Electric Vehicle (EV) data and includes advanced data visualizations using Plotly, along with a dynamic racing bar chart showcasing the growth of EV manufacturers over the last ten years.

## Table of Contents
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Performing EDA](#performing-eda)
- [Visualizations using Plotly](#visualizations-using-plotly)
- [Visualizations using Racing Bar Chart](#visualizations-using-racing-bar-chart)


## Installation
Open your terminal and then run this command to install jupyter lab
        
    pip install jupyter lab

#### Clone this Repository 
If the repository on github, Clone it to your local machine

    git clone https://github.com/Aadityaganesh/Electric_vehicles  

#### Launch jupyter lab
Launch juypter lab in terminal by running the following command

    jupyter lab

## Project Structure:

Here's the brief desription about the  Electric Vehicles dataset
- **VIN:** The Vehicle Identification Number is a unique alphanumeric code assigned to each vehicle for identification purposes. This column represents the first 10 characters of the VIN.
- **County:** The county where the vehicle is registered in Washington State.
- **City:** The city where the vehicle is registered in Washington State.
- **State:** The state where the vehicle is registered (Washington in this case).
- **Postal Code:** The postal code of the registration address for the vehicle.
- **Model Year:** The year in which the vehicle was manufactured.
- **Make:** The manufacturer or brand of the vehicle.
- **Model:** The specific model or name of the vehicle.
- **Electric Vehicle Type:** Indicates whether the vehicle is a Battery Electric Vehicle (BEV) or a Plug-in Hybrid Electric Vehicle (PHEV).
- **Clean Alternative Fuel Vehicle (CAFV) Eligibility:** Indicates if the vehicle meets the eligibility criteria for Clean Alternative Fuel Vehicle incentives or benefits.
- **Electric Range:** The distance the vehicle can travel on electric power alone, typically measured in miles.
- **Base MSRP:** The Manufacturer's Suggested Retail Price, which is the starting price set by the vehicle manufacturer.
- **Legislative District:** The legislative district associated with the vehicle's registered address.
- **DOL Vehicle ID:** A unique identifier assigned by the Washington State Department of Licensing (DOL) for each registered vehicle.
- **Vehicle Location**: The precise location of the vehicle, which could be the address or coordinates.
- **Electric Utility**: The name of the electric utility company associated with the vehicle, if applicable.
- **2020 Census Tract**:The census tract associated with the vehicle's registered address, based on the 2020 Census data.


## Performing EDA

#### Necessary libraries 
To work on this analysis you need to ensure that, you have installed these python libraries

    !pip install numpy
    !pip install pandas
    !pip install matplotlib
    !pip install seaborn

Make sure all libraries are installed and they are working properly while your are working on this analysis
    
Conducted an in-depth Exploratory Data Analysis (EDA) of the dataset, focusing on both univariate and multivariate relationships to uncover valuable insights.

Here are some useful DataFrame functions for initial exploration:

- **df.info():** Provides a concise summary of the DataFrame, including the number of non-null entries and data types.

- **df.shape:** Returns the dimensions of the DataFrame as a tuple (number of rows, number of columns).

- **df.columns:** This is used to check the name of columns in a dataframe.

- **df.head():** Displays the first five rows of the DataFrame for a quick preview of the data.

- **df.duplicated():** Returns a boolean Series indicating whether each row is a duplicate.

- **df.isna().sum():** Calculates the total number of missing values in each column.

**Handling Missing Values**

#### Before Handling missing values

The following table presents the sum count of missing values in each column:
| Field                                                   | Count |
|---------------------------------------------------------|-------|
| VIN (1-10)                                             | 0     |
| County                                                 | 0     |
| City                                                   | 0     |
| State                                                  | 0     |
| Postal Code                                            | 0     |
| Model Year                                             | 0     |
| Make                                                   | 0     |
| Model                                                  | 20    |
| Electric Vehicle Type                                  | 0     |
| Clean Alternative Fuel Vehicle (CAFV) Eligibility      | 0     |
| Electric Range                                         | 0     |
| Base MSRP                                              | 0     |
| Legislative District                                   | 286   |
| DOL Vehicle ID                                         | 0     |
| Vehicle Location                                       | 24    |
| Electric Utility                                       | 443   |
| 2020 Census Tract                                      | 0     |

In the electric vehicle dataset, we encountered several missing values across different columns. To ensure data integrity and avoid issues during analysis, we applied the following strategies for filling these missing values:

- **Model:**

Missing values in the Model column were replaced with the string 'Unknown'. This approach allows us to maintain the integrity of the dataset while clearly indicating that the model information was not available.

    df['Model'] = df['Model'].fillna('Unknown')
        
- **Legislative District:**

Missing values in the Legislative District column were replaced with 0. This numerical replacement indicates the absence of a valid legislative district and allows for easier aggregation or analysis later.

    df['Legislative District'] = df['Legislative District'].fillna(0)

- **Vehicle Location:**

Similar to the Model column, missing values in the Vehicle Location were filled with the string 'Unknown' to maintain dataset completeness while denoting the lack of specific location data.

    df['Vehicle Location'] = df['Vehicle Location'].fillna('Unknown')
        
- **Electric Utility:**

For the Electric Utility column, we used the mode (the most frequently occurring value) to fill missing values. This method ensures that we replace missing data with a representative value, thus preserving the overall distribution of the dataset.

    df['Electric Utility'] = df['Electric Utility'].fillna(df['Electric Utility'].mode()[0])
        
By addressing missing values using these strategies, we ensured that our analysis could proceed without complications related to incomplete data.

#### After handling missing values

The following table presents the sum count of missing values in each column:
| Field                                                   | Count |
|---------------------------------------------------------|-------|
| VIN (1-10)                                             | 0     |
| County                                                 | 0     |
| City                                                   | 0     |
| State                                                  | 0     |
| Postal Code                                            | 0     |
| Model Year                                             | 0     |
| Make                                                   | 0     |
| Model                                                  | 0     |
| Electric Vehicle Type                                  | 0     |
| Clean Alternative Fuel Vehicle (CAFV) Eligibility      | 0     |
| Electric Range                                         | 0     |
| Base MSRP                                              | 0     |
| Legislative District                                   | 0     |
| DOL Vehicle ID                                         | 0     |
| Vehicle Location                                       | 0     |
| Electric Utility                                       | 0     |
| 2020 Census Tract                                      | 0     |


**Univariate Analysis**
  
- **Distribution of Electric Vehicle Types:**

    - A pie chart was created to visualize the distribution of different electric vehicle types. This chart displays the percentage of each type, providing a clear overview of the dataset's composition.
        
        df['Electric Vehicle Type'].value_counts().plot.pie(autopct='%1.1f%%', startangle=90)
        plt.title('Distribution of Electric Vehicle Types')
        plt.show()
  
- **Boxplot of Legislative District:**

    - A horizontal boxplot was generated to analyze the distribution of legislative districts. This visualization helps identify any outliers or variations in data across districts.
    
            plt.figure(figsize=(10, 6))
            sns.boxplot(data=df['Legislative District'], orient='h')
            plt.title('Boxplot of Legislative District')
            plt.xlabel('Legislative District')
            plt.show()
  
- **Electric Range Distribution:**

    - A histogram with a kernel density estimate (KDE) was plotted to examine the distribution of the electric range of vehicles. This visualization highlights the range and frequency of electric ranges within the dataset.
    
            plt.figure(figsize=(10, 6))
            sns.histplot(df['Electric Range'], bins=20, kde=True)
            plt.title('Distribution of Electric Range')
            plt.show()
  
- **Make Count Distribution:**

    - A count plot was created to visualize the frequency of various makes of electric vehicles. This chart provides insight into which manufacturers dominate the market in the dataset.
    
            plt.figure(figsize=(15, 10))
            sns.countplot(data=df, x='Make')
            plt.xticks(rotation=90)
            plt.xlabel('Make')
            plt.ylabel('Count')
            plt.show()
  
**Bivariate Analysis**

- **Electric Range vs. Base MSRP:**

    - A scatter plot was generated to explore the relationship between electric range and base MSRP, with points colored by electric vehicle type. This visualization helps identify potential correlations and patterns between these two numerical variables.
      
            plt.figure(figsize=(10, 6))
            sns.scatterplot(x='Electric Range', y='Base MSRP', hue='Electric Vehicle Type', data=df)
            plt.title('Electric Range vs Base MSRP')
            plt.show()
  
- **Model Year vs. Base MSRP:**

    - A boxplot was created to analyze the relationship between model year and base MSRP. This visualization allows for comparison of the price distribution across different model years.
    
            plt.figure(figsize=(10, 6))
            sns.boxplot(x='Model Year', y='Base MSRP', data=df)
            plt.title('Model Year vs Base MSRP')
            plt.xticks(rotation=45)
            plt.show()

**Multivariate Analysis**

- **Correlation Heatmap:**
    - A heatmap was generated to visualize the correlation matrix of numerical features. This analysis highlights the strength and direction of relationships between different numerical variables, aiding in understanding how these features interact with one another.
      
            numeric_df = df.select_dtypes(include=['float64', 'int64'])
            corr_matrix = numeric_df.corr()
            plt.figure(figsize=(10, 6))
            sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', linewidths=0.5, vmin = -1, vmax =1 )
            plt.title('Correlation Heatmap')
            plt.show()

## Visualizations using Plotly

* Created interactive and visually engaging plots using Plotly to present the data in a meaningful and interpretable way.
  Note for Visualizing Electric Vehicle Count by State
  
- To visualize the number of electric vehicles (EVs) by state using Plotly in Jupyter Lab, follow these steps:

- **Install Plotly:**
      If you haven't installed Plotly yet, use the following command in a Jupyter cell:

      !pip install plotly
  
- **Setting Up Plotly for Jupyter Lab:**
    To ensure proper display of interactive visualizations, set the default renderer in Jupyter Lab as follows:
    
      import plotly.io as pio
      pio.renderers.default = 'iframe'
      
- Create the Choropleth Map: Use the following code to generate a choropleth map of the number of EVs by state:

        ev_count_by_state = df.groupby('State').size().reset_index(name='EV Count')
        fig = px.choropleth(
            ev_count_by_state,
            locations='State',
            locationmode='USA-states',
            color='EV Count',
            scope="usa",
            color_continuous_scale="Viridis",
            title="Number of EV Vehicles by State",
            labels={'EV Count': 'Number of EVs'}
        )
        fig.show()
![Screenshot 2024-10-12 191409](https://github.com/user-attachments/assets/f32a0d42-ee61-4fde-84af-e5f963278eaf)
- This code will generate an interactive choropleth map displaying the distribution of electric vehicles across different states in the USA.

## Visualizations using Racing Bar Chart

* Developed a dynamic racing bar chart to visualize the growth of Electric Vehicle manufacturers over time.

This project includes a dynamic bar chart race visualization to illustrate the changing counts of electric vehicle makes over the years. The animation highlights trends and shifts in the electric vehicle market.

**Installation**

To run the bar chart race, ensure you have the required libraries installed. You can install the bar-chart-race library using:

    !pip install bar-chart-race

**Code Overview**

The following code processes the electric vehicle dataset and creates a horizontal bar chart race:

    import bar_chart_race as bcr
    from IPython.display import Image, display
    import pandas as pd
    
    # Assuming 'Model Year' is in numeric format, first convert it if necessary
    df['Model Year'] = pd.to_numeric(df['Model Year'], errors='coerce')
    
    # Filter the data for the last 10 years
    recent_years = df['Model Year'].max() - 10
    df_last_10_years = df[df['Model Year'] >= recent_years]
    
    # Convert 'Model Year' back to string for grouping and visualization
    df_last_10_years['Model Year'] = df_last_10_years['Model Year'].astype(str)
    
    # Group the data by 'Model Year' and 'Make' to get the count
    grouped_data = df_last_10_years.groupby(['Model Year', 'Make']).size().reset_index(name='Count')
    
    # Pivot the data for the bar chart race
    pivoted_data = grouped_data.pivot(index='Model Year', columns='Make', values='Count').fillna(0)
    
    # Create the bar chart race and save it as a .gif
    bcr.bar_chart_race(
        df=pivoted_data, 
        filename='EV_make_racing_bar_plot_last_10_years.gif',  # Saves as .gif
        orientation='h', 
        sort='desc', 
        n_bars=10, 
        title='EV Make Count Over the Last 10 Years in States of USA', 
        filter_column_colors=True,  
        period_length=1000
    )
    
    # Display the .gif
    Image(filename='EV_make_racing_bar_plot_last_10_years.gif')

#### Display the .gif in the Jupyter notebook
    Image(filename='EV_make_racing_bar_plot.gif')
Visualization
The resulting GIF, EV_make_racing_bar_plot.gif, showcases the number of electric vehicles by make for each model year, providing insights into the growth and popularity of various electric vehicle manufacturers.
![EV_make_racing_bar_plot_last_10_years](https://github.com/user-attachments/assets/94a1a37e-4993-419a-9654-809ff472192f)

