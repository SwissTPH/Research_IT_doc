# ODK Quick Start Guide

**ODK** (Open Data Kit) enables user-friendly digital data collection in the field. It connects **form designers**, **data collectors**, and **analysts** through a shared ODK Central server.

## 🔦ODK Workflow at a Glance

**For form designers**:

Design questionnaire using **XLSForm** ➡️ Upload to **ODK Central** ➡️ (Wait for collectors to submit) ➡️ View data and manage **datasets/entities**

**For data collectors**:

Download blank forms via **ODK Collect** ➡️ Fill in and submit forms ➡️ Auto-upload to **ODK Central** when online



## 🧩Components

| Component       | Description                                             | Typical User              |
| --------------- | ------------------------------------------------------- | ------------------------- |
| **XLSForm**     | Excel-based questionnaire design file (`.xlsx`)         | Form designer             |
| **ODK Central** | Web platform for form hosting, user and data management | Project manager / analyst |
| **ODK Collect** | Android app for field data entry and submission         | Data collector            |



## 🚀Quick Steps

**For Designers**

1. Create your form using ODK’s [XLSForm template](https://docs.getodk.org/xlsform/) in `.xlsx` (`survey`, `choices`, and `settings` sheets).
2. Upload the `.xlsx` file to **ODK Central** under "Forms" tab "New".
3. Publish the form and share access with data collectors.
4. Monitor submissions via the "Entities" tab.

**For Collectors**

1. Install **ODK Collect**.
2. Download available forms.
3. Fill in the forms offline; submissions will auto-upload when connected to the internet.



## 📊Viewing data

1. Log in to **ODK Central** ➡️ "Forms" ➡️ "Submissions" or **ODK Central** ➡️ "Entities" to review records.
2. Export data as `.csv` or connect to tools like R (RuODK) or Python (PyODK) for analysis.



## 🔗Other useful links

- [ODK quick start guide from WHO](https://cdn.who.int/media/docs/default-source/classification/other-classifications/autopsy/2022-va-instrument/odk4va-quick-guide-v2-2025-designed.pdf?sfvrsn=c1425ce0_1&download=true)
- [ODK official website](https://docs.getodk.org/getting-started/)
- [ODK forum](https://forum.getodk.org/)