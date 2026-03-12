# Flexion Code Review

**Temperature Validation Tool — ServiceNow**

A ServiceNow application that allows lab technicians and medical staff to validate temperature readings converted between Kelvin, Celsius, Fahrenheit, and Rankine. The tool uses the UCUM web service as the authoritative conversion source and compares the result against a user-reported reading, accounting for significant figures.

**Prerequisites**

A ServiceNow instance (any recent release — tested on Washington DC)
Admin access to import update sets
The instance must be able to make outbound HTTP calls to https://ucum.nlm.nih.gov

**Installation**

1. Log in to your ServiceNow instance as an admin.
2. Navigate to System Update Sets > Retrieved Update Sets.
3. Click Import Update Set from XML.
4. Upload the file Update Set XML File from this repo.
5. Open the imported update set named Temperature_Validator_MB.
6. Click Preview Update Set and resolve any conflicts if prompted.
7. Click Commit Update Set.

This will create all the required components listed below.

**Accessing the Application**

After committing the update set, open your browser and go to:
https://<your-instance>.service-now.com/temperature_validator.do
Replace <your-instance> with your ServiceNow instance name.

**How to Use**

Enter the Input Value (the temperature reading to convert, e.g. 84.2).
Select the Input Unit (the unit the value is currently in).
Select the Target Unit (the unit to convert to).
Enter the Reported Reading (the value you want to validate against).
Click Validate.
The system will display one of three results:

Correct — the reported reading matches the converted value (after rounding to the appropriate significant figures).
Incorrect — the reported reading does not match.
Invalid — the input value or reported reading is not a number, or the unit is not recognized.

**Prioritized Next Steps**
