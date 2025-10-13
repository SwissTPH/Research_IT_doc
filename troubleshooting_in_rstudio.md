# Troubleshooting in RStudio

## SSL Connect Error When Installing Packages

It is suggested to use R versions provided at Software Center supported by Swiss TPH IT to avoid SSL Connect Error. If you have several R versions installed on your computer, please make sure that you have the correct R version specified by checking the following steps:

1. Open RStudio, go to "Tools - Global Options - General".

2. Make sure you have the correct R version chosen. Current Swiss TPH default version should be "[64-bit] C:\Program Files\R\R-4.4.1".

3. If it's not the Swiss TPH version, go to "Change - Choose a specific version of R", and select "[64-bit] C:\Program Files\R\R-4.4.1".

4. Save and apply all the changes, and restart RStudio.

![Change R Version](images\SSL_Connect_Error.PNG)

## Troubleshooting Performance Issues in RStudio

If you experience a sudden drop in performance when using RStudio (e.g., sluggish behavior on startup), the issue is related to RStudio itself, not to any R installation that you have on your laptop (having several R versions should not impact performance).

These steps should help resolve common RStudio performance issues. If problems persist, consider further troubleshooting or seeking guidance from the [Posit Community forum](https://forum.posit.co/).

1. Check your Home working directory
   
   1. Ensure that your home working directory is local
   
   2. Run the following command in your R console to check: Sys.getenv(“HOME”)

2. Disable workspace save/restore
   
   1. Go to *Tools* **>** *Global Options*
   
   2. In the *General* panel under the *Basic* tab:
      
      - Uncheck *Restore .RData into workspace at startup*
      
      - Set *Save workspace to .RData on exit* to *Never*
   
   3- Apply the changes
   
   4- Close and restart RStudio (may also be good to reboot to be sure changes are indeed applied)

3- Disable auto-diagnosis

   1- Go to *Tools* **>** *Global Options*

   2- Navigate to *Code* **>** Diagnostics

   3- Uncheck *Show diagnostics for R*

   4- Apply the changes

   5- Close and restart RStudio

   *If performance improves, it is likely caused by an issue with your R code.*

4- Change rendering engine

   1- Go to *Tools* > *Global Options*

   2- Navigate to *General* > *Advanced*

   3- Set *Rendering Engine* to *Software*

   4- Apply the changes

   5- Restart RStudio

5- Inspect profile files

   Examine your user profile settings to identify any configuration options that might override global settings (e.g. in your .Rprofile).
