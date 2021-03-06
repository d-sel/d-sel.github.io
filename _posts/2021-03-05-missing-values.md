### Missing Data: Why should we care and how can we deal with it?

The vast majority of the time, we are trying to make conclusions about
something using imperfect data. These imperfections can be in the form
of typos, values that require additional calculations and missing data
points. Typos and inconsistencies can be dealt with as we can ‘find and
replace’ to clean them up and perform simple calculations to convert
them to something that is meaningful for our purposes. However, with
missing data, we cannot replace something that is not there. Plus, if we
have to work with the given data, we have to make use of what we have.

Missing data can be present under different names: as blank space in a
spreadsheet, any form of ‘N/A’ wording or even as the word ‘null’. If we
have missing data, can we just ignore those rows and work with the rest?
Although easy to do, this can affect our results.

### Impact of Missing Data

To illustrate how missing data can impact results, we will look at an
example based off [Employee Job Satisfaction data from
Kaggle.com](https://www.kaggle.com/mohamedharris/employee-satisfaction-index-dataset).
We have a company employee survey and we want to determine which of the
three departments has the most satisfied employees. The data shows the
department the employee belongs to, how they were recruited, and their
satisfaction response. Employees who were satisfied responded ‘True’ and
those who weren’t responded ‘False’. Our data has 300 responses and 10
are shown here for context.

    ## # A tibble: 10 x 4
    ##       X1 Dept       recruitment_type   satisfied
    ##    <dbl> <chr>      <chr>              <lgl>    
    ##  1     0 Purchasing Walk-in            FALSE    
    ##  2     1 HR         Walk-in            TRUE     
    ##  3     2 Purchasing Recruitment Agency FALSE    
    ##  4     3 HR         Walk-in            TRUE     
    ##  5     4 Sales      On-Campus          FALSE    
    ##  6     5 HR         On-Campus          TRUE     
    ##  7     6 Purchasing Recruitment Agency FALSE    
    ##  8     7 HR         On-Campus          TRUE     
    ##  9     8 Sales      Referral           TRUE     
    ## 10     9 HR         On-Campus          TRUE

The impact on results relates to the reason the data is missing: 1)
***Completely at random***: The chance of any particular data point
missing is the same. We cannot find any patterns to the missing data and
can equally expect any of the rows or columns to have a missing data
point.

1.  ***Pattern within the data itself***: Data can be missing but have a
    pattern to it that can be identified from the data we have. For
    example, if we have data that is collected during the day, we may
    notice that during specific hours, we are missing certain columns in
    the data. We would be able to pinpoint this as we would have a
    column in our data identifying the time.

2.  ***Pattern outside of our data***: Similar to the second type, data
    can be missing with a pattern, but it can be related to something
    that is not captured within our data columns. This is the most
    difficult to identify as we cannot see the pattern directly.

<u>Scenario 1:</u> Our survey data is complete! We have no missing data.

    ## # A tibble: 2 x 5
    ##   X1        satisfied    HR Purchasing Sales
    ##   <chr>     <lgl>     <dbl>      <dbl> <dbl>
    ## 1 satisfied FALSE       0.5      0.43   0.45
    ## 2 satisfied TRUE        0.5      0.570  0.55

We have summarized the responses by department in the table above. We
can see that the department responding with the highest satisfaction is
Purchasing, with 57% of respondents indicating that they are satisfied
at their work. Next was Sales with 55% and lastly, HR with exactly half
reporting as satisfied.

<u>Scenario 2:</u> Our survey data has missing responses, but it’s
completely random.

    ## # A tibble: 2 x 5
    ##   X1        satisfied    HR Purchasing Sales
    ##   <chr>     <lgl>     <dbl>      <dbl> <dbl>
    ## 1 satisfied FALSE       0.5      0.43  0.43 
    ## 2 satisfied TRUE        0.5      0.570 0.570

Compared to our first scenario where we have no missing data, our
results are generally similar. The percentages will fluctuate, but they
are not very different.

<u>Scenario 3:</u> Our survey data has missing responses, but there is a
pattern to it.

    ## # A tibble: 2 x 5
    ##   X1        satisfied    HR Purchasing Sales
    ##   <chr>     <lgl>     <dbl>      <dbl> <dbl>
    ## 1 satisfied FALSE      0.49       0.45  0.39
    ## 2 satisfied TRUE       0.51       0.55  0.61

In this scenario, there is a pattern to the missing data. If we could
examine our data in detail, we would discover that most of the missing
values were in the responses from Sales department employees who had
been recruited On-Campus or using a Recruitment Agency. It turned out
that they were more likely to not respond than to indicate that they
were not satisfied because they were new hires. These patterns are
usually context specific. A situation where there was a pattern outside
of our data would be similar, except that we could not see it from the
data we had. For instance, if there was a computer problem on the last
day of the survey and parts of the responses from that day were not
saved properly but we had no column indicating the day the employees
filled out the survey.

If we take the approach of ignoring rows with missing responses, we
overstate our percentage of satisfied employees. We can see that the
percentage of Sales employees reporting as satisfied is up to 61%,
higher than both Scenario 1 and 2.

### Fixing Missing Data

Once we have determined the type of missing data, we can now deal with
it appropriately:

-   If our data is missing completely at random (scenario 2), then it is
    safe to ignore those rows. Prior to doing any sort of calculations
    with the data, we safely eliminate those rows and continue our work.

-   If our missing data has a pattern within or outside of the dataset
    (scenario 3), we cannot ignore the rows. Instead, we should fill
    them with an appropriate value. This process is called imputation
    and there are many approaches that can be taken, some of which are
    simpler and others that require statistical calculations.

With numeric data, one of the simple approaches we can take is to
populate the missing values of a column using the mean or mode (most
frequent) of that column’s existing data. An approach with text data is
to group the rows and give all of the missing values within the same
group the same value which helps to reflect some of the differences
across groups which may provide more accuracy over using one value
across the whole dataset.

### Conclusion

Missing data is something we all have to deal with; although it may not
seem like an important aspect of our work, we must consider the
importance of dealing with it properly or at least being aware of how
our results may be affected. Once we classify our missing data, we can
decide how to best deal with it. The simple approaches are usually
sufficient, and if we decide that more complex methods are needed, we
can explore more complex statistical approaches.
