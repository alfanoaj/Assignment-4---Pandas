
# PyCity Schools Analysis
Observed Trend 1: Charter schools produce better results than district schools.
Observed Trend 2: As schools get smaller, the results get better.
Observed Trend 3: Interestingly enough, the results get worse as the budget per student increases.  Perhaps smaller schools don't have as much leniency in their budget, but have a greater rate of success with a smaller student-to-teacher ratio?


```python
#import dependencies
import pandas as pd
```


```python
#store filepaths as variables
school_file = "raw_data/schools_complete.csv"
student_file = "raw_data/students_complete.csv"
```


```python
#read datafiles with the pandas library
school_df = pd.read_csv(school_file)
student_df = pd.read_csv(student_file)
```


```python
#Show the header for the schools file
school_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Show the header for the student file
student_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>



# District Analysis


```python
#Identify incomplete rows in the school df
school_df.count()
```




    School ID    15
    name         15
    type         15
    size         15
    budget       15
    dtype: int64




```python
#Identify incomplete rows in the student df
student_df.count()
```




    Student ID       39170
    name             39170
    gender           39170
    grade            39170
    school           39170
    reading_score    39170
    math_score       39170
    dtype: int64




```python
#calculates the count of schools and sets the school_count variable
school_count = school_df["name"].count()
print(school_count)
```

    15
    


```python
#calculates the count of students and sets the student_count variable
student_count = student_df["name"].count()
student_count = int(student_count)
print(student_count)
```

    39170
    


```python
#calculates total budget and sets the total_budget variable
total_budget = school_df["budget"].sum()
total_budget = int(total_budget)
print(total_budget)
```

    24649428
    


```python
#calculates average math score and sets avg_math variable
avg_math = student_df["math_score"].mean()
avg_math = float(avg_math)
print(avg_math)
```

    78.98537145774827
    


```python
#calculates average reading score and sets avg_reading variable
avg_reading = student_df["reading_score"].mean()
avg_reading = float(avg_reading)
print(avg_reading)
```

    81.87784018381414
    


```python
#calculates the % of students passing math and sets passing_math_percentage variable (70% or greater was considered passing)
passing_math_df = student_df.loc[student_df["math_score"]>=70]
math_passing_count = passing_math_df["math_score"].count()
print(math_passing_count)
passing_math_percentage = math_passing_count/student_count
passing_math_percentage = float(passing_math_percentage*100)
print(passing_math_percentage)
```

    29370
    74.9808526933878
    


```python
#calculates the % of students passing reading and sets passing_reading_percentage variable (70% or greater was considered passing)
passing_reading_df = student_df.loc[student_df["reading_score"]>=70]
reading_passing_count = passing_reading_df["reading_score"].count()
print(reading_passing_count)
passing_reading_percentage = reading_passing_count/student_count
passing_reading_percentage = float(passing_reading_percentage*100)
print(passing_reading_percentage)
```

    33610
    85.80546336482001
    


```python
#calculates the overall passing rate and sets passing_rate variable (70% or greater was considered passing)
passing_rate = (passing_math_percentage + passing_reading_percentage)/2
passing_rate = float(passing_rate)
print(passing_rate)
```

    80.39315802910392
    


```python
#creates a dataframe of the district's key metrics
district_df = pd.DataFrame(
    {"Total Schools": [school_count],
     "Total Students": [student_count],
     "Total Budget": [total_budget],
     "Average Math Score": [avg_math],
     "Average Reading Score": [avg_reading],
     "% Passing Math": [passing_math_percentage],
     "% Passing Reading": [passing_reading_percentage],
     "Overall Passing Rate": [passing_rate]
    }
)
district_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>80.393158</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
#cleans up and maps the variables in the district_df
district_df["% Passing Math"] = district_df["% Passing Math"].map("{:.2f}%".format)
district_df["% Passing Reading"] = district_df["% Passing Reading"].map("{:.2f}%".format)
district_df["Average Math Score"] = district_df["Average Math Score"].map("{:.2f}%".format)
district_df["Average Reading Score"] = district_df["Average Reading Score"].map("{:.2f}%".format)
district_df["Overall Passing Rate"] = district_df["Overall Passing Rate"].map("{:.2f}%".format)
district_df["Total Budget"] = district_df["Total Budget"].map("${:,.0f}".format)
district_df["Total Students"] = district_df["Total Students"].map("{:,.0f}".format)
district_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74.98%</td>
      <td>85.81%</td>
      <td>78.99%</td>
      <td>81.88%</td>
      <td>80.39%</td>
      <td>$24,649,428</td>
      <td>15</td>
      <td>39,170</td>
    </tr>
  </tbody>
</table>
</div>




```python
#organizing the df to make it easier to read
organized_district_df = district_df[["Total Schools", "Total Students", "Total Budget", "Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "Overall Passing Rate"]]
organized_district_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428</td>
      <td>78.99%</td>
      <td>81.88%</td>
      <td>74.98%</td>
      <td>85.81%</td>
      <td>80.39%</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary


```python
#rename the headings in the df to clean it up
renamed_school_df = school_df.rename(columns={"name": "School Name", "type": "Type", "size": "Student Count", "budget": "Total Budget"})
renamed_school_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>School Name</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Groups the student df based on the school column and then sets a new df for the mean of those scores
grouped_student_df = student_df.groupby(["school"], as_index = False)
student_mean = grouped_student_df["school", "reading_score", "math_score"].mean()
student_mean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
#rename school column in the student_mean df for a merge with the renamed_school_df
renamed_student_mean = student_mean.rename(columns={"school":"School Name", "reading_score":"Average Reading Score", "math_score":"Average Math Score"})
renamed_student_mean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merges the renamed_student_mean and renamed_school_df
school_df_merge = pd.merge(renamed_student_mean, renamed_school_df, on="School Name")
school_df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>School ID</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
  </tbody>
</table>
</div>




```python
#calculates the per student budget and adds it to the school_df_merge
school_df_merge["Budget Per Student"] = school_df_merge["Total Budget"]/school_df_merge["Student Count"]
school_df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>School ID</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Uses a groupby on the passing math df then performs the calculation and adds it to the school df merge
passing_math_count = passing_math_df.groupby(["school"], as_index=False)
passing_math = passing_math_count["math_score"].count()
school_df_merge["% Passing Math"] = passing_math["math_score"]/school_df_merge["Student Count"]*100
school_df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>School ID</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>% Passing Math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>66.680064</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>94.133477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>65.988471</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>68.309602</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>93.392371</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>66.752967</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>92.505855</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>65.683922</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>66.057551</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>94.594595</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>66.366592</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>93.867121</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>93.272171</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>93.867718</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>93.333333</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Uses a groupby on the passing reading df then performs the calculation and adds it to the school df merge
passing_reading_count = passing_reading_df.groupby(["school"], as_index=False)
passing_reading = passing_reading_count["reading_score"].count()
school_df_merge["% Passing Reading"] = passing_reading["reading_score"]/school_df_merge["Student Count"]*100
school_df_merge
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>School ID</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>66.680064</td>
      <td>81.933280</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>94.133477</td>
      <td>97.039828</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>65.988471</td>
      <td>80.739234</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>68.309602</td>
      <td>79.299014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>93.392371</td>
      <td>97.138965</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>66.752967</td>
      <td>80.862999</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>92.505855</td>
      <td>96.252927</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>65.683922</td>
      <td>81.316421</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>66.057551</td>
      <td>81.222432</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>94.594595</td>
      <td>95.945946</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>66.366592</td>
      <td>80.220055</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>93.867121</td>
      <td>95.854628</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>93.272171</td>
      <td>97.308869</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>93.867718</td>
      <td>96.539641</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>93.333333</td>
      <td>96.611111</td>
    </tr>
  </tbody>
</table>
</div>




```python
#calculates/adds in the overall passing rate to the above dataframe and sets/sorts the index on School ID
school_df_merge["Overall Passing Rate"] = (school_df_merge["% Passing Math"]+school_df_merge["% Passing Reading"])/2
master_school_df = school_df_merge.set_index("School Name").sort_index()
final_school_df = school_df_merge.set_index("School Name").sort_index()
master_school_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>School ID</th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Format the data in the columns of the dataframe
master_school_df["% Passing Math"] = master_school_df["% Passing Math"].map("{:.2f}%".format)
master_school_df["% Passing Reading"] = master_school_df["% Passing Reading"].map("{:.2f}%".format)
master_school_df["Average Reading Score"] = master_school_df["Average Reading Score"].map("{:.2f}%".format)
master_school_df["Average Math Score"] = master_school_df["Average Math Score"].map("{:.2f}%".format)
master_school_df["Total Budget"] = master_school_df["Total Budget"].map("${:,.0f}".format)
master_school_df["Student Count"] = master_school_df["Student Count"].map("{:,.0f}".format)
master_school_df["Budget Per Student"] = master_school_df["Budget Per Student"].map("${:,.0f}".format)
master_school_df["Overall Passing Rate"] = master_school_df["Overall Passing Rate"].map("{:.2f}%".format)
master_school_df = master_school_df[["Type", "Student Count", "Total Budget", "Budget Per Student", "Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "Overall Passing Rate"]]
master_school_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4,976</td>
      <td>$3,124,928</td>
      <td>$628</td>
      <td>77.05%</td>
      <td>81.03%</td>
      <td>66.68%</td>
      <td>81.93%</td>
      <td>74.31%</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1,858</td>
      <td>$1,081,356</td>
      <td>$582</td>
      <td>83.06%</td>
      <td>83.98%</td>
      <td>94.13%</td>
      <td>97.04%</td>
      <td>95.59%</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2,949</td>
      <td>$1,884,411</td>
      <td>$639</td>
      <td>76.71%</td>
      <td>81.16%</td>
      <td>65.99%</td>
      <td>80.74%</td>
      <td>73.36%</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2,739</td>
      <td>$1,763,916</td>
      <td>$644</td>
      <td>77.10%</td>
      <td>80.75%</td>
      <td>68.31%</td>
      <td>79.30%</td>
      <td>73.80%</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1,468</td>
      <td>$917,500</td>
      <td>$625</td>
      <td>83.35%</td>
      <td>83.82%</td>
      <td>93.39%</td>
      <td>97.14%</td>
      <td>95.27%</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4,635</td>
      <td>$3,022,020</td>
      <td>$652</td>
      <td>77.29%</td>
      <td>80.93%</td>
      <td>66.75%</td>
      <td>80.86%</td>
      <td>73.81%</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087</td>
      <td>$581</td>
      <td>83.80%</td>
      <td>83.81%</td>
      <td>92.51%</td>
      <td>96.25%</td>
      <td>94.38%</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2,917</td>
      <td>$1,910,635</td>
      <td>$655</td>
      <td>76.63%</td>
      <td>81.18%</td>
      <td>65.68%</td>
      <td>81.32%</td>
      <td>73.50%</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4,761</td>
      <td>$3,094,650</td>
      <td>$650</td>
      <td>77.07%</td>
      <td>80.97%</td>
      <td>66.06%</td>
      <td>81.22%</td>
      <td>73.64%</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>$609</td>
      <td>83.84%</td>
      <td>84.04%</td>
      <td>94.59%</td>
      <td>95.95%</td>
      <td>95.27%</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3,999</td>
      <td>$2,547,363</td>
      <td>$637</td>
      <td>76.84%</td>
      <td>80.74%</td>
      <td>66.37%</td>
      <td>80.22%</td>
      <td>73.29%</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1,761</td>
      <td>$1,056,600</td>
      <td>$600</td>
      <td>83.36%</td>
      <td>83.73%</td>
      <td>93.87%</td>
      <td>95.85%</td>
      <td>94.86%</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1,635</td>
      <td>$1,043,130</td>
      <td>$638</td>
      <td>83.42%</td>
      <td>83.85%</td>
      <td>93.27%</td>
      <td>97.31%</td>
      <td>95.29%</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2,283</td>
      <td>$1,319,574</td>
      <td>$578</td>
      <td>83.27%</td>
      <td>83.99%</td>
      <td>93.87%</td>
      <td>96.54%</td>
      <td>95.20%</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1,800</td>
      <td>$1,049,400</td>
      <td>$583</td>
      <td>83.68%</td>
      <td>83.95%</td>
      <td>93.33%</td>
      <td>96.61%</td>
      <td>94.97%</td>
    </tr>
  </tbody>
</table>
</div>



# Top Performing Schools (By Passing Rate)


```python
top_performing_schools = master_school_df.sort_values(by=["Overall Passing Rate"], ascending = False).head()
top_performing_schools
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1,858</td>
      <td>$1,081,356</td>
      <td>$582</td>
      <td>83.06%</td>
      <td>83.98%</td>
      <td>94.13%</td>
      <td>97.04%</td>
      <td>95.59%</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1,635</td>
      <td>$1,043,130</td>
      <td>$638</td>
      <td>83.42%</td>
      <td>83.85%</td>
      <td>93.27%</td>
      <td>97.31%</td>
      <td>95.29%</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1,468</td>
      <td>$917,500</td>
      <td>$625</td>
      <td>83.35%</td>
      <td>83.82%</td>
      <td>93.39%</td>
      <td>97.14%</td>
      <td>95.27%</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>$609</td>
      <td>83.84%</td>
      <td>84.04%</td>
      <td>94.59%</td>
      <td>95.95%</td>
      <td>95.27%</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2,283</td>
      <td>$1,319,574</td>
      <td>$578</td>
      <td>83.27%</td>
      <td>83.99%</td>
      <td>93.87%</td>
      <td>96.54%</td>
      <td>95.20%</td>
    </tr>
  </tbody>
</table>
</div>



# Bottom Performing Schools (By Passing Rate


```python
bottom_performing_schools = master_school_df.sort_values(by=["Overall Passing Rate"], ascending = True).head()
bottom_performing_schools
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Student Count</th>
      <th>Total Budget</th>
      <th>Budget Per Student</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3,999</td>
      <td>$2,547,363</td>
      <td>$637</td>
      <td>76.84%</td>
      <td>80.74%</td>
      <td>66.37%</td>
      <td>80.22%</td>
      <td>73.29%</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2,949</td>
      <td>$1,884,411</td>
      <td>$639</td>
      <td>76.71%</td>
      <td>81.16%</td>
      <td>65.99%</td>
      <td>80.74%</td>
      <td>73.36%</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2,917</td>
      <td>$1,910,635</td>
      <td>$655</td>
      <td>76.63%</td>
      <td>81.18%</td>
      <td>65.68%</td>
      <td>81.32%</td>
      <td>73.50%</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4,761</td>
      <td>$3,094,650</td>
      <td>$650</td>
      <td>77.07%</td>
      <td>80.97%</td>
      <td>66.06%</td>
      <td>81.22%</td>
      <td>73.64%</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2,739</td>
      <td>$1,763,916</td>
      <td>$644</td>
      <td>77.10%</td>
      <td>80.75%</td>
      <td>68.31%</td>
      <td>79.30%</td>
      <td>73.80%</td>
    </tr>
  </tbody>
</table>
</div>



# Math Scores By Grade


```python
#Creates a new df for the average math grade by school and grade
renamed_student_df = student_df.rename(columns={"school":"School", "grade":"Grade", "math_score": "Average Math Score", "reading_score":"Average Reading Score"})
ninth_grade_df = renamed_student_df.loc[renamed_student_df["Grade"] == "9th"]
tenth_grade_df= renamed_student_df.loc[renamed_student_df["Grade"] == "10th"]
eleventh_grade_df= renamed_student_df.loc[renamed_student_df["Grade"] == "11th"]
twelvth_grade_df= renamed_student_df.loc[renamed_student_df["Grade"] == "12th"]
ninth_grade_average = ninth_grade_df.groupby(["School"], as_index=False).mean()
tenth_grade_average = tenth_grade_df.groupby(["School"], as_index=False).mean()
eleventh_grade_average = eleventh_grade_df.groupby(["School"], as_index=False).mean()
twelvth_grade_average = twelvth_grade_df.groupby(["School"], as_index=False).mean()
math_master = ninth_grade_average[["School", "Average Math Score"]]
math_master = math_master.rename(columns={"Average Math Score":"9th"})
math_master["10th"] = tenth_grade_average[["Average Math Score"]]
math_master["11th"] = eleventh_grade_average[["Average Math Score"]]
math_master["12th"] = twelvth_grade_average[["Average Math Score"]]
math_master = math_master.set_index("School")
math_master["9th"] = math_master["9th"].map("{:.2f}%".format)
math_master["10th"] = math_master["10th"].map("{:.2f}%".format)
math_master["11th"] = math_master["11th"].map("{:.2f}%".format)
math_master["12th"] = math_master["12th"].map("{:.2f}%".format)
math_master
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.08%</td>
      <td>77.00%</td>
      <td>77.52%</td>
      <td>76.49%</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.09%</td>
      <td>83.15%</td>
      <td>82.77%</td>
      <td>83.28%</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.40%</td>
      <td>76.54%</td>
      <td>76.88%</td>
      <td>77.15%</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.36%</td>
      <td>77.67%</td>
      <td>76.92%</td>
      <td>76.18%</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.04%</td>
      <td>84.23%</td>
      <td>83.84%</td>
      <td>83.36%</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.44%</td>
      <td>77.34%</td>
      <td>77.14%</td>
      <td>77.19%</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.79%</td>
      <td>83.43%</td>
      <td>85.00%</td>
      <td>82.86%</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.03%</td>
      <td>75.91%</td>
      <td>76.45%</td>
      <td>77.23%</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.19%</td>
      <td>76.69%</td>
      <td>77.49%</td>
      <td>76.86%</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.63%</td>
      <td>83.37%</td>
      <td>84.33%</td>
      <td>84.12%</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.86%</td>
      <td>76.61%</td>
      <td>76.40%</td>
      <td>77.69%</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.42%</td>
      <td>82.92%</td>
      <td>83.38%</td>
      <td>83.78%</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.59%</td>
      <td>83.09%</td>
      <td>83.50%</td>
      <td>83.50%</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.09%</td>
      <td>83.72%</td>
      <td>83.20%</td>
      <td>83.04%</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.26%</td>
      <td>84.01%</td>
      <td>83.84%</td>
      <td>83.64%</td>
    </tr>
  </tbody>
</table>
</div>



# Reading Scores By Grade


```python
#Create a new df for the average reading grade by student grade
reading_master = ninth_grade_average[["School", "Average Reading Score"]]
reading_master = reading_master.rename(columns={"Average Reading Score":"9th"})
reading_master["10th"] = tenth_grade_average[["Average Reading Score"]]
reading_master["11th"] = eleventh_grade_average[["Average Reading Score"]]
reading_master["12th"] = twelvth_grade_average[["Average Reading Score"]]
reading_master = reading_master.set_index("School")
reading_master["9th"] = reading_master["9th"].map("{:.2f}%".format)
reading_master["10th"] = reading_master["10th"].map("{:.2f}%".format)
reading_master["11th"] = reading_master["11th"].map("{:.2f}%".format)
reading_master["12th"] = reading_master["12th"].map("{:.2f}%".format)
reading_master
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.30%</td>
      <td>80.91%</td>
      <td>80.95%</td>
      <td>80.91%</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.68%</td>
      <td>84.25%</td>
      <td>83.79%</td>
      <td>84.29%</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.20%</td>
      <td>81.41%</td>
      <td>80.64%</td>
      <td>81.38%</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.63%</td>
      <td>81.26%</td>
      <td>80.40%</td>
      <td>80.66%</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.37%</td>
      <td>83.71%</td>
      <td>84.29%</td>
      <td>84.01%</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.87%</td>
      <td>80.66%</td>
      <td>81.40%</td>
      <td>80.86%</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.68%</td>
      <td>83.32%</td>
      <td>83.82%</td>
      <td>84.70%</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.29%</td>
      <td>81.51%</td>
      <td>81.42%</td>
      <td>80.31%</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.26%</td>
      <td>80.77%</td>
      <td>80.62%</td>
      <td>81.23%</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.81%</td>
      <td>83.61%</td>
      <td>84.34%</td>
      <td>84.59%</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.99%</td>
      <td>80.63%</td>
      <td>80.86%</td>
      <td>80.38%</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.12%</td>
      <td>83.44%</td>
      <td>84.37%</td>
      <td>82.78%</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.73%</td>
      <td>84.25%</td>
      <td>83.59%</td>
      <td>83.83%</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.94%</td>
      <td>84.02%</td>
      <td>83.76%</td>
      <td>84.32%</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.83%</td>
      <td>83.81%</td>
      <td>84.16%</td>
      <td>84.07%</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Spending


```python
#gather information on the final_school_df to set up bins
final_school_df["Budget Per Student"].describe()
```




    count     15.000000
    mean     620.066667
    std       28.544368
    min      578.000000
    25%      591.500000
    50%      628.000000
    75%      641.500000
    max      655.000000
    Name: Budget Per Student, dtype: float64




```python
#create our bins for spending by student and groups data into bins from final_school_df
spending_bins = [575, 595, 615, 635, 655]
spending_bin_names = ["<$595", "$595-615","$615-635", "$635<"]
pd.cut(final_school_df["Budget Per Student"], spending_bins, labels=spending_bin_names)
```




    School Name
    Bailey High School       $615-635
    Cabrera High School         <$595
    Figueroa High School        $635<
    Ford High School            $635<
    Griffin High School      $615-635
    Hernandez High School       $635<
    Holden High School          <$595
    Huang High School           $635<
    Johnson High School         $635<
    Pena High School         $595-615
    Rodriguez High School       $635<
    Shelton High School      $595-615
    Thomas High School          $635<
    Wilson High School          <$595
    Wright High School          <$595
    Name: Budget Per Student, dtype: category
    Categories (4, object): [<$595 < $595-615 < $615-635 < $635<]




```python
#create a new df for the bins analysis
spending_df = final_school_df[["Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "Overall Passing Rate"]]
spending_df["Spending Rating"] = pd.cut(final_school_df["Budget Per Student"], spending_bins, labels=spending_bin_names)
grouped_spending_df = spending_df.groupby(["Spending Rating"])
final_spending_df = grouped_spending_df.mean()
final_spending_df
```

    C:\Users\alfan\AppData\Local\conda\conda\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Rating</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$595</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>93.460096</td>
      <td>96.610877</td>
      <td>95.035486</td>
    </tr>
    <tr>
      <th>$595-615</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>94.230858</td>
      <td>95.900287</td>
      <td>95.065572</td>
    </tr>
    <tr>
      <th>$615-635</th>
      <td>80.199966</td>
      <td>82.425360</td>
      <td>80.036217</td>
      <td>89.536122</td>
      <td>84.786170</td>
    </tr>
    <tr>
      <th>$635&lt;</th>
      <td>77.866721</td>
      <td>81.368774</td>
      <td>70.347325</td>
      <td>82.995575</td>
      <td>76.671450</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Size


```python
#gather information on the range of school size for grouping into bins
final_school_df["Student Count"].describe()
```




    count      15.000000
    mean     2611.333333
    std      1420.915282
    min       427.000000
    25%      1698.000000
    50%      2283.000000
    75%      3474.000000
    max      4976.000000
    Name: Student Count, dtype: float64




```python
#create our bins for school size and groups data into bins from final_school_df
size_bins = [0, 1800, 3400, 5000]
size_bin_names = ["Small", "Medium", "Large"]
pd.cut(final_school_df["Student Count"], size_bins, labels=size_bin_names)
```




    School Name
    Bailey High School        Large
    Cabrera High School      Medium
    Figueroa High School     Medium
    Ford High School         Medium
    Griffin High School       Small
    Hernandez High School     Large
    Holden High School        Small
    Huang High School        Medium
    Johnson High School       Large
    Pena High School          Small
    Rodriguez High School     Large
    Shelton High School       Small
    Thomas High School        Small
    Wilson High School       Medium
    Wright High School        Small
    Name: Student Count, dtype: category
    Categories (3, object): [Small < Medium < Large]




```python
size_df = final_school_df[["Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "Overall Passing Rate"]]
size_df["Size Rating"] = pd.cut(final_school_df["Student Count"], size_bins, labels=size_bin_names)
grouped_size_df = size_df.groupby(["Size Rating"])
final_size_df = grouped_size_df.mean()
final_size_df
```

    C:\Users\alfan\AppData\Local\conda\conda\envs\PythonData\lib\site-packages\ipykernel\__main__.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Size Rating</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small</th>
      <td>83.575787</td>
      <td>83.867683</td>
      <td>93.494241</td>
      <td>96.518741</td>
      <td>95.006491</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>79.355974</td>
      <td>82.210453</td>
      <td>77.596638</td>
      <td>86.986827</td>
      <td>82.291733</td>
    </tr>
    <tr>
      <th>Large</th>
      <td>77.063340</td>
      <td>80.919864</td>
      <td>66.464293</td>
      <td>81.059691</td>
      <td>73.761992</td>
    </tr>
  </tbody>
</table>
</div>



# Score by School Type


```python
type_df = final_school_df[["Type","Average Math Score", "Average Reading Score", "% Passing Math", "% Passing Reading", "Overall Passing Rate"]]
grouped_type_df = type_df.groupby(["Type"])
final_type_df = grouped_type_df.mean()
final_type_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>93.620830</td>
      <td>96.586489</td>
      <td>95.103660</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>66.548453</td>
      <td>80.799062</td>
      <td>73.673757</td>
    </tr>
  </tbody>
</table>
</div>


