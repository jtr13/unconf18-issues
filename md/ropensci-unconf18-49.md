# [Percentiles and z scores in maternal child health](https://github.com/ropensci/unconf18/issues/49)

> state: **open** opened by: **monicagerber** on: **5/7/2018**

I often need to calculate percentiles, z scores, and other measures of growth in maternal &amp; child health research. There are some SAS macros out there and a couple of R packages. The 2 R packages I found don&#x27;t have all of the measures I need and are a bit clunky to use with tidyverse packages. There are other measures that don&#x27;t have a SAS macro or R package, just a data table of LMS parameters in a manuscript (PDF). Ideally these methods would be available all in one place in an R package!

Here some things the package could calculate:

1. Percentiles and z scores for BMI using the CDC reference charts (SAS program: https://www.cdc.gov/nccdphp/dnpao/growthcharts/resources/sas.htm). I&#x27;ve found 1 package (childsds) that does this, but does not have all of the options as the SAS macro. Importantly, it doesn&#x27;t calculate %BMIp95 (percent of the 95th percentile of BMI), which is being used more in obesity research. The zscorer package only uses WHO growth charts. The CDC charts are standard in US pediatric obesity research. I have been in contact with the author of the SAS macro and he is very nice and fully supportive of turning this into an R package!

2. Birth weight for gestational age z-score. I haven&#x27;t seen a publicly available program for this. I use a SAS program copied from another analyst. (Ref: Oken, E., Kleinman, K. P., Rich-Edwards, J., &amp; Gillman, M. W. (2003). A nearly continuous measure of birth weight for gestational age using a United States national reference. BMC pediatrics, 3(1), 6.) 

3. Child blood pressure percentiles.  (https://sites.google.com/a/channing.harvard.edu/bernardrosner/pediatric-blood-press/childhood-blood-pressure/childhoodbppctsas)

Eventually this could also include measures of maternal gestational weight gain.

After speaking with Stefanie about this, it seems like this could be a good project for someone who hasn&#x27;t made an R package (myself included). The calculations aren&#x27;t too difficult.   

### Comments

