# Power BI (install)

# Power BI installation of JobManager BI

There are two versions for **SaaS** and **OnPrem**. Below is help for both versions. General knowledge of setting up Power BI is a prerequisite.

## SaaS BC

It is recommended to make initial [setup of BI statistics groups](../advanced-setup/power-bi.md).

### Setup the report

1.  Open the included Power BI template `JobManager_BI_SaaS.pbit`  
    _The file is located in the "BI" folder of the JobManager nstallationsfilen (ZIP)._
    
2.  Specify connection parameters.  
    Hover over the (i) icons next to the individual parameters for instructions/examples.
    
3.  Click “Load”
    
4.  Power BI prompts you to sign in to your Business Central account
    
5.  Click “Connect”  
      
    The report will load data from Business Central  
    Check out the built-in RLS roles. Users must be assigned to a role to use the report in the Power BI Service. The roles are as follows:
    
    *   _All_: All data available
    *   _All except pay_: All data available except pay entries.
    *   _Calc. responsible_: All data for the employees, that the logged in user is calculation responsible for.
    *   _Calc. responsible except pay_: All data for the employees, that the logged in user is calculation responsible for except pay entries.  
          
        
6.  Set the default date range by changing the “Filter on all pages: CurYearOffset”  
    E.g. `Greater than -5` (Default value) corresponds to _previous 4 yeas + current year_.
    
7.  Save the report as a `.PBIX` file
    
8.  Publish the report to the Power BI Service
    
9.  Assign AAD groups or individual users to the RLS roles on the semantic model
    
10.  Configure scheduled refresh in the Power BI Service
     
11.  _Optional:_ Publish the report as a app to give your audience the best reporting experience
     

## OnPrem NAV/BC (SQL version)

1.  Open the file `JobManager_BI_OnPrem.pbit`.  
    _The file is located in the "BI" folder of the JobManager nstallationsfilen (ZIP)._
    
2.  Enter parameters:
    *   `SqlServer`: Server name or IP
    *   `SqlDataBase`: BC/NAV database name
    *   `RangeStart`: Enter default value as in _info bubble_ on then field.
    *   `RangeEnd`: Enter default value as in _info bubble_ on then field.
    *   `BaseAppID`: Enter as given in the _info bubble_ on the field.
    *   `JmgAppDI`: Enter as given in the _info bubble_ on the field.
3.  Choose `Load`.
    
4.  Publish the raport to PBI Service.
    
5.  Setup RLS on dataset in the Power BI service (On the dataset select menu item `Security`)  
    Users/AD-groups is added to the individual RLS groups:
    *   `All`: Can see all
    *   `All except pay`: Can see all - except payroll information
    *   `Calc. responsible`: Can see all on the employees for which the user has the Time Calculation responsibility.
    *   `Calc. responsible except pay`: Can see all on the employees for which the user has the Time Calculation responsibility - except payroll
6.  [Setup the report in BC/NAV](../advanced-setup/power-bi.md).
    
7.  Update the dataset in PBI.
    

## See also

[Power BI](../advanced-setup/power-bi.md)
