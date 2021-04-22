# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.



## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
1. PDF report generator from the analyzed data. 
1. Notification utility when new report is available

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | This is not part of analysis of data, it is data conversion
Counting the breaches       | Yes           | This is part of analysis of data 
Detecting trends            | Yes           | The trends are expected to be analyzed and recorded 
Notification utility        | No            | This is type of alert utility not analysis of data 

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
1. Write "Invalid input" to the PDF when the csv doesn't contain expected data (could be due to communication error/Null pointer) 
1. Write "count of breach" to the PDF from a csv containing readings when threshold is crossed
1. Write "trends elements date & time" to the PDF when the reading was continuously increasing for 30 minutes
2. Write test to see if notification utility is called when new PDF report is available.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input                   | Output                                                 | Faked/mocked part
|--------------------------|-------------------------|--------------------------------------------------------|---
Read input from server     | csv file                | internal data-structure                                | Fake the server store
Validate input             | csv data                | valid / invalid                                        | None - it's a pure function
Notify report availability | no input                | Event success flag updated / email sent                | mock the notification function
Report inaccessible server | no input                | Communication error flag updated / email sent          | mock reporting/notifying inaccessible server 
Find minimum and maximum   | csv data                | Analyzed data_structure (min max element)              | None - it's a pure function
Detect trend               | csv data                | Analyzed data-structure (trend element)                | None - it's a pure function
Write to PDF               | Analyzed data structure | Variable to state success of event & generated PDF file| Mock PDF generation  
