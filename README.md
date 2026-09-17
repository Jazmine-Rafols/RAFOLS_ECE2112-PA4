# **ECE2112: Programming Assessment 4**
**Submitted by: Jazmine Mikaela L. Rafols | 2ECE-D**   
**Submitted on: September 10, 2026**

## **Objectives of the Experiment**
> At the end of Programming Assessment 4, the student should be able to filter tabular data using categorical and numerical conditions, construct focused DataFrames by selecting relevant features, summarize the relationship between categorical features and a numerical variable, and communicate a data comparison using clear and correctly labeled plots. The **ECE Board Exam 2** dataset shall be used for the experiment proper and require the use of `Pandas` and a Python plotting library in executing the experiment.

## A. Visayas Communication DataFrame
> **Instructions:** Create a DataFrame named `VisComm` containing students whose `Hometown` is `Visayas` and whose `Track` is `Communication` based on the `ECE_BoardExam_2` dataset. When retrieving the selected students under these conditions, retain only the following columns in their respective order: `Name`, `Gender`, `Math`, `Electronics`, and `Average`. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

Before creating the DataFrame `VisComm`, it is necessary to display the main dataset `ECE_BoardExam_2` first to have a reference on what the DataFrame will call and what the expected results should appear. Thus, the experiment shall start with initializing the `Pandas` library,
```python
import pandas as pd
```
From there, `Pandas` can be utilized to load the `excel` file of the main dataset, where it will display 30 rows of students and contains eight columns such as: `Name`, `Gender`, `Track`, `Hometown`, `Math`, `Electronics`, `GEAS`, and `Communication`.

### Solution to the Problem

Now that the main dataset has been defined, the first DataFrame `VisComm` can be executed. First, in order to retrieve the `Average` of the main DataFrame, it must be first defined within `ECE_BoardExam_2`; where it will add an additional column to the DataFrame. However, to compute for the average, the Pandas function `.mean()` can be used to acquire the row-wise mean of each student,
```python
ECE_BoardExam_2['Average'] = ECE_BoardExam_2[['Math','Electronics','GEAS','Communication']].mean(axis=1)
```
Then, the DataFrame 'VisComm' is asked to contain students whose `Hometown` is `Visayas` **and** whose `Track` is `Communications`. The condition `and` calls on the use of the AND operator, or denoted as `&` in the experiment. 

To find the corresponding students inclusive of these conditions, the `loc` or locate property of `Pandas` can be used to select specific data and modify using *label-based* indexing, where it uses the name of a row, column, or value to manipulate the data. This can be seen demonstrated below,
```python
VisComm = ECE_BoardExam_2.loc[(ECE_BoardExam_2['Hometown']=='Visayas')&(ECE_BoardExam_2['Track']=='Communication'), ['Name','Gender','Math','Electronics','Average']]
VisComm
```
As demonstrated, the students who fulfill the conditions of their `Hometown` being `Visayas` and whose `Track` is `Communication` are retrieved through calling the labels of their features and using the equivalence operator `==`, which checks the values of two expressions or variables if they are equal.

The names following the comma after the two main conditions are the retained columns from the main dataset. These columns are handpicked from the main dataset to be displayed along with the selected students as requested by the problem.

The results should display a total of five students, meaning the shape of `VisComm` is `5` as it pertains to its rows. It should be displayed as shown below,

| | Name | Gender | Math | Electronics | Average |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **10** | S11 | Female | 48 | 56 | 54.75 |
| **11** | S12 | Male | 89 | 67 | 76.00 |
| **17** | S18 | Male | 81 | 40 | 63.50 |
| **21** | S22 | Female | 64 | 39 | 62.50 |
| **27** | S28 | Male | 85 | 53 | 67.75 |

Where the total number of rows in `VisComm` is displayed by,
```python
print("Total number of rows in DataFrame, VisComm: ", VisComm.shape[0])
```

## B. Visayas Female DataFrame
> **Instructions:**  Create a second DataFrame named `VisFemale` containing the students whose `Hometown` is `Visayas` and whose `Gender` is `Female` based on the `ECE_BoardExam_2` dataset. Retain only the following columns: `Name`, `Track`, `GEAS`, `Electronics`, and `Average`. Display `VisFemale`, then display only the rows of `VisFemale` whose `Average` is at least 60. In doing so, do not overwrite `VisFemale` when performing the second filter.

Similarly to problem A, a second DataFrame named `VisFemale` should contain students whose `Hometown` is `Visayas`. However, its second condition in place of the track is looking for students whose `Gender` is `Female`.

### Solution to the Problem

As with problem A, the condition is explicitly `Visayas` AND `Female`, which entails that the use of the and operator `&` is required. Following earlier’s solution with the use of the `loc` property of `Pandas` and using label-based indexing to indicate where and which features to check if the values are true or false using the equivalence `==` operator, problem B utilizes an identical solution to the problem. Although, it has another exception where the retained columns are the following: `Name`, `Track`, `GEAS`, `Electronics`, and `Average`. The DataFrame `VisFemale` should appear as follows,
```python
VisFemale = ECE_BoardExam_2.loc[(ECE_BoardExam_2['Hometown']=='Visayas')&(ECE_BoardExam_2['Gender']=='Female'), ['Name','Track','GEAS','Electronics','Average']]
VisFemale
```
Printing `VisFemale` should return a total of six students under the applied conditions,

| | Name | Track | GEAS | Electronics | Average |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5** | S6 | Microelectronics | 86 | 45 | 75.50 |
| **10** | S11 | Communication | 48 | 56 | 54.75 |
| **20** | S21 | Microelectronics | 68 | 51 | 68.50 |
| **21** | S22 | Communication | 89 | 39 | 63.50 |
| **23** | S24 | Microelectronics | 60 | 45 | 57.75 |
| **25** | S24 | Instrumentation | 83 | 47 | 65.75 |

The second requirement for problem B asks for the number of `Female` students whose `Average` is greater or equal to `>=`, coined by “at least”, 60. This following condition should return a lessened number of four students. The final output of `VisFemale` is,

| | Name | Track | GEAS | Electronics | Average |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **5** | S6 | Microelectronics | 86 | 45 | 75.50 |
| **20** | S21 | Microelectronics | 68 | 51 | 68.50 |
| **21** | S22 | Communication | 89 | 39 | 63.50 |
| **25** | S24 | Instrumentation | 83 | 47 | 65.75 |

## C. Category-Average Visualization
> **Instructions:** Examine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`. For each feature, compute the mean of `Average` for every category using `Pandas` then display the three summary tables. Using these values, create one figure that contains three bar charts: mean Average by Track, by Gender, and by Hometown. Following the figure, write three concise statements identifying the category with the highest sample mean for each feature. However, describe the observed dataset only. Note that differences in group means does not imply the cause of a higher score.

For problem C, to display the data of the aforementioned dataset in the form of charts is a property of the Python library `matplotlib`, a data-visualization tool for Python. To use this feature, it must be first initialized as,
```python
import matplotlib.pyplot as plt
```
With this initialization, it will allow the use of a variety of data-processing and visualization tools to execute.

### Solution to the Problem

Firstly, the mean of `Average` of the selected categories `Track`, `Gender`, and `Hometown` must be taken, which can be executed using the `pivot_table` tool. The data-processing tool `pivot_table` essentially calculates and performs arithmetic procedures on raw data, acting as a spreadsheet and summarizing them. This feature allows the user to analyze data either numerically or visually through comparisons in patterns or trends in data.

Acknowledging the purpose of the `pivot_table` tool, the mean of the `Average` for `Track` was calculated using this tool. Its index was assigned to `Track` to acquire the values of `Average`. Applying the `reset_index()` allows a clean display of the modified index while still retaining the old index.

The default syntax that will be used for remaining two other categories shall be,
```python
Average_Track = ECE_BoardExam_2.pivot_table(index='Track', values = 'Average').reset_index()
Average_Track
```
Then, by applying this syntax to the rest of the categories and changing their index to their respective category, the returned tables of values should be as follows:

For the category `Track`,

| | Track | Average |
| :--- | :--- | :--- |
| **0** | Communication | 67.975 |
| **1** | Instrumentation | 65.225 |
| **2** | Microelectronics | 67.500 |

For the category `Gender`,

| | Gender | Average |
| :--- | :--- | :--- |
| **0** | Female | 66.616667 |
| **1** | Male | 67.183333 |

For the category `Hometown`,

| | Hometown | Average |
| :--- | :--- | :--- |
| **0** | Luzon | 68.083333 |
| **1** | Visayas | 66.678571 |
| **2** | Mindanao | 65.750000 |

After acquiring the necessary data, these can be plotted visually using `plt.figure` and configured by its figure size `figsize`, which is set to 15 by 4 to accommodate the large bar charts to be displayed horizontally and in one figure. It is then followed by `plt.bar` to create the bar chart itself followed by the dataset it will call on which is the mean of the averages by categories taken earlier.

`plt.subplot` refers to the placement and dimensions of a chart in the form of a grid system. The first variable represents the total number of rows, the second variable represents the total number of columns, and the third variable represents the active plot index or placement of the chart.

As per the requirements of problem C, the charts need their respective x and y labels and titles for appropriate readability, which are named accordingly to their corresponding data. It is then tidied by the last method `plt.tight_layout()`, which ensures that the charts do not overlap and remain readable.

The solution is demonstrated below,
```python
plt.figure(figsize=(15,4))

plt.subplot(1,3,1)
plt.bar(Average_Track['Track'], Average_Track['Average'])
plt.title('Average by Track')
plt.xlabel('Track')
plt.ylabel('Average')

plt.subplot(1,3,2)
plt.bar(Average_Gender['Gender'], Average_Gender['Average'])
plt.xlabel('Gender')
plt.ylabel('Average')
plt.title('Average by Gender')

plt.subplot(1,3,3)
plt.bar(Average_Hometown['Hometown'], Average_Hometown['Average'])
plt.xlabel('Hometown')
plt.ylabel('Average')
plt.title('Average by Hometown')

plt.tight_layout()
```
After analyzing the generated bar charts, the interpretation of the three charts is written below. It is important to note that the interpretation of the charts are mere observations and not a direct answer as to why the scores are the way they are due to certain features. The three listed interpretations are contained under `interpretation` for easier retrieval, shown as follows,
```python
interpretation = (
    "Interpretation \n"
    "1.) When taking the mean of Average by Track, the category of students with the highest sample mean is Communication, with an average of 67.98. \n"
    "2.) When taking the mean of Average by Gender, it is observed that Male students demonstrated the highest sample mean, with an average of 67.18. \n"
    "3.) When taking the mean of Average by Hometown, it is observed that students from Luzon have the highest sample mean, with an average of 68.08."
)
```
Then, it is displayed under the figure using `plt.figtext` followed by its position axes of (`0.01`, `-0.12`), a font size of 11, and a horizontal alignment to the left-side. These are set for appropriate readability for the user as it will be displayed through `plt.show()`.
```python
plt.figtext(0.01, -0.12, interpretation, fontsize=11, ha='left')
plt.show()
```
The figure should appear as so,
<img width="1500" height="400" alt="Category-Average Figure" src="https://github.com/user-attachments/assets/03c4fb5f-de30-480c-94ad-8631baa860d5" />

As the interpretation cannot be seen in the figure, here is the complete version of the interpretation.

1.) When taking the mean of Average by Track, the category of students with the highest sample mean is Communication, with an average of **67.98**. \
2.) When taking the mean of Average by Gender, it is observed that Male students demonstrated the highest sample mean, with an average of **67.18**. \
3.) When taking the mean of Average by Hometown, it is observed that students from Luzon have the highest sample mean, with an average of **68.08**.
- - -
### **Thank you for Reading!**
To view the complete program for Programming Assessment 4, refer to this link: [Programming Assessment 4 by Jazmine Rafols](https://github.com/Jazmine-Rafols/RAFOLS_ECE2112-PA4/blob/37a1275c05af518672a9751214e85173078897b9/Program_Assessment-4.ipynb)
### File Version History 
September 10, 2026 - Initial upload (draft) of the README file. \
September 12, 2026 - Upload of the complete version of the README file. \
September 17, 2026 - Rewrote README due to error in ipynb file and its execution.
