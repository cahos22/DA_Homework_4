
# District Summary

#Create a high level snapshot (in table form) of the district's key metrics, including:

Total Schools

Total Students

Total Budget

Average Math Score

Average Reading Score

% Passing Math

% Passing Reading

Overall Passing Rate (Average of the above two)


```python
# Dependencies
import pandas as pd
import os

```


```python
# Read csv into DataFrame

# Create a reference the CSV file desired
schools_csv_path = os.path.join('raw_data', 'schools_complete.csv')


# Read the CSVs into a Pandas DataFrame
schools_raw_df = pd.read_csv(schools_csv_path)




schools_raw_df.head()



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

# Create a reference the CSV file desired
students_csv_path = os.path.join('raw_data', 'students_complete.csv')

# Read the CSVs into a Pandas DataFrame
students_raw_df = pd.read_csv(students_csv_path)

students_raw_df.dtypes

students_raw_df.head()


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




```python
percentage_pass_math = students_raw_df.loc[students_raw_df["math_score"]>60,
                                           ["math_score"]].count()


```


```python
percentage_pass_read = students_raw_df.loc[students_raw_df["reading_score"]>60,
                                           "reading_score"].count()
percentage_pass_read
```




    39170




```python
# Generating high level snapshot
students_raw_df.dtypes

total_schools = schools_raw_df["School ID"].count()
total_students = students_raw_df["Student ID"].count()
total_budget = schools_raw_df["budget"].sum()
avg_math_score = students_raw_df["math_score"].mean()
avg_read_score = students_raw_df["reading_score"].mean()
percentage_pass_math = (len(students_raw_df.loc[students_raw_df["math_score"]>60,
                                           ["math_score"]]) / total_students) * 100

percentage_pass_read = (len(students_raw_df.loc[students_raw_df["reading_score"]>60,
                                           "reading_score"]) / total_students) * 100


overall_passing_rate = (percentage_pass_math + percentage_pass_read) / 2


percentage_pass_math
percentage_pass_read
district_metrics_df = pd.DataFrame([{"Total Schools":total_schools,
                                    "Total Students":total_students,
                                    "Total Budget":total_budget,
                                    "Average Math Score":avg_math_score,
                                    "Average Reading Score":avg_read_score,
                                    "% Passing Math":percentage_pass_math,
                                    "% Passing Reading":percentage_pass_read,
                                    "Overall Passing Rate":overall_passing_rate}
                                   ])


district_metrics_df


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
      <td>90.906306</td>
      <td>100.0</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>95.453153</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary

## Create an overview table that summarizes key metrics about each school, including:
### School Name
### School Type
### Total Students
### Total School Budget
### Per Student Budget
### Average Math Score
### Average Reading Score
### % Passing Math
### % Passing Reading
### Overall Passing Rate (Average of the above two)


```python
renamed_school_df = schools_raw_df.rename(columns={"name":"school"})
school_student_merged=pd.merge(renamed_school_df, students_raw_df, on="school")


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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39165</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>39165</td>
      <td>Donna Howard</td>
      <td>F</td>
      <td>12th</td>
      <td>99</td>
      <td>90</td>
    </tr>
    <tr>
      <th>39166</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>39166</td>
      <td>Dawn Bell</td>
      <td>F</td>
      <td>10th</td>
      <td>95</td>
      <td>70</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>73</td>
      <td>84</td>
    </tr>
    <tr>
      <th>39168</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>39168</td>
      <td>Desiree Kidd</td>
      <td>F</td>
      <td>10th</td>
      <td>99</td>
      <td>90</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>39169</td>
      <td>Carolyn Jackson</td>
      <td>F</td>
      <td>11th</td>
      <td>95</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>




```python
grp_school=school_student_merged.groupby("school")
school_type=grp_school["type"]
total_student_count=grp_school["Student ID"].count()
grp_school_budget=grp_school["budget"].sum()
per_student_budget=grp_school_budget / total_student_count
school_math_score = grp_school["math_score"].mean()
school_read_score = grp_school["reading_score"].mean()
stud_count = grp_school.count()
count_stud_pass_math= stud_count.loc[stud_count["math_score"]>60,:] 
count_stud_pass_reading= stud_count.loc[stud_count["reading_score"]>60,:] 

percent_studs_pass_math = (count_stud_pass_math / stud_count) * 100
percent_studs_pass_reading =(count_stud_pass_reading / stud_count) * 100

overall_pass_rate= (percent_studs_pass_math["math_score"] + percent_studs_pass_reading["reading_score"])/2

school_summary=pd.DataFrame({"School Type" : school_type,
                            "Total Students":total_student_count,
                            "Total School Budget":grp_school_budget,
                            "Per Student Budget":per_student_budget,
                            "Average Math Score":school_math_score,
                            "Average Reading Score":school_read_score,
                            "% Passing Math":percent_studs_pass_math["math_score"],
                            "% Passing Reading":percent_studs_pass_reading["reading_score"],
                            "Overall Passing Rate":overall_pass_rate})
school_summary.head()
#total_student_count.head()
#per_student_budget.head()

#overview_school_df=pd.DataFrame(grpby_obj)
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
      <th>Per Student Budget</th>
      <th>School Type</th>
      <th>Total School Budget</th>
      <th>Total Students</th>
    </tr>
    <tr>
      <th>school</th>
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
      <td>100.0</td>
      <td>100.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>100.0</td>
      <td>3124928.0</td>
      <td>(Bailey High School, [District, District, Dist...</td>
      <td>15549641728</td>
      <td>4976</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>100.0</td>
      <td>100.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.0</td>
      <td>1081356.0</td>
      <td>(Cabrera High School, [Charter, Charter, Chart...</td>
      <td>2009159448</td>
      <td>1858</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>100.0</td>
      <td>100.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>100.0</td>
      <td>1884411.0</td>
      <td>(Figueroa High School, [District, District, Di...</td>
      <td>5557128039</td>
      <td>2949</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>100.0</td>
      <td>100.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>100.0</td>
      <td>1763916.0</td>
      <td>(Ford High School, [District, District, Distri...</td>
      <td>4831365924</td>
      <td>2739</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>100.0</td>
      <td>100.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.0</td>
      <td>917500.0</td>
      <td>(Griffin High School, [Charter, Charter, Chart...</td>
      <td>1346890000</td>
      <td>1468</td>
    </tr>
  </tbody>
</table>
</div>


