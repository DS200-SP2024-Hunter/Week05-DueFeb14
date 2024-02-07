# Lab Assignment for Week 05
## Creating interactive maps using folium
## Due on [Canvas](https://psu.instructure.com/courses/2306358/assignments/15960975) on Wed., Feb. 14 at 11:59pm

**On this and all labs for the rest of the semester: When you have a choice between the [datascience package](https://www.data8.org/datascience/) and the [pandas library](https://pandas.pydata.org/docs/), you are free to use either method to complete your work.** _For this lab #5, we recommend using the datascience package._

The main objective of today's lab is to produce a map of Penn State University's campuses based on the tools presented in [Section 8.5](https://inferentialthinking.com/chapters/08/5/Bike_Sharing_in_the_Bay_Area.html) in the textbook. You will also need to use the `join` and `group` methods presented in [Sections 8.4](https://inferentialthinking.com/chapters/08/4/Joining_Tables_by_Columns.html) and [8.5](https://inferentialthinking.com/chapters/08/5/Bike_Sharing_in_the_Bay_Area.html), which are extremely important data-handling skills.

When you turn in your work, it should not contain any irrelevant text and code boxes from the textbook Jupyter notebooks. Please delete text and code boxes unrelated to the assignment before you upload your lab.


**Objective**:  Produce two maps of Pennsylvania on which you plot the location of each campus using pins or circles, as in [Section 8.5](https://inferentialthinking.com/chapters/08/5/Bike_Sharing_in_the_Bay_Area.html), where you can use size (radius) and/or color to indicate statistics about each campus.

Your assignment is as follows:

1. Download the two .csv files in this repository using the `read_table` method in Section 8.5. (You should try to mimic the code that creates the `trips` object in that Jupyter notebook, but make changes to the name of the object and the filenames to suit the purpose of this lab). Here are the two full URLs for the files:
   
```
https://raw.githubusercontent.com/DS200-SP2024-Hunter/Week05-DueFeb14/main/PSUCampusLocations.csv
https://raw.githubusercontent.com/DS200-SP2024-Hunter/Week05-DueFeb14/main/PSUDemographicDataFA2023.csv
```

One of these files is a database of latitude and longitude locations of each campus, while the other is a table with more than 48000 rows that counts students in broken down by various categories, including location. You should give the Table objects you create sensible names.


**NEED TO EDIT BELOW THIS LINE**

2. Create a map using only the smaller Table. To do this, first relabel the columns in this table using the `relabel` method so that their names are `lat`, `long`, and `labels`.  For instance, if your Table is called `LocationTable`, then you would use the following code to do the relabeling:

```
LocationTable.relabel('Lat', 'lat')
LocationTable.relabel('Long', 'long')
LocationTable.relabel('Campus', 'labels')
```

It turns out that the `Marker.map_table` method requires a table with columns in exactly the correct ordering (`lat` then `long` then `labels`), so you can perform this reordering using
```
LocationTable = LocationTable.select('lat','long','labels')
```
(Remember, all of the above code supposes that you've named your smaller object `LocationTable`.  You should change the code to match your own object's name.) Once the Table has only three columns, in the correct order with the correct labels, you can simply use this code that is taken from Section 8.5:
```
Marker.map_table(LocationTable)
```   
3. Use the `join` method to create a new (very large!) Table object in which each row contains both the student information and the latitude/longitude positions of their campuses. Make sure you include the code that performs this step in your work that you turn in.  Also, use the `labels` method (as in `MyTableObjectName.labels`) to disply the names of your new, joined Table object.

4. Group the rows in your large Table object according to the campus location using `MyTableObjectName.group('Location')`.  Give this grouped object a name, then print it out in its entirety using the `show()` method, as in:

```
GroupedByCampus = MyTableObjectName.group('Location')
GroupedByCampus.show()
```

5. Create a new map using circles where the radius of each circle is controled by the `count` column in your grouped object.  See Section 8.5 for guidance on how this works. If you wish, add colors.

6. [Optional for an extra point:] Group according to location as well as some other column of interest to you. Compute some interesting new statistic for each campus, then produce a new map that somehow conveys this information.

7. [Optional for an extra point:] Take the `Enrollment Count` information into account. The information in step 5 is not quite giving total enrollments because each row in the table represents one OR MORE students.  Figure out a way to incorporate these counts so that you are correctly plotting actual enrollment numbers.

When you've completed this, you should select "Print" from the File menu, then somehow save to pdf using this option.  The pdf file that you create in this way is the file that you should upload to Canvas for grading.  Recall that sometimes the right side of the notebooks are chopped off by this print procedure, but we have found that if you can select the "A3" paper size from the advanced options, this seems to solve the problem.

