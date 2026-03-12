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

1) Add stronger client-side validation
Right now most validation happens on the server. I would add additional checks in the UI so invalid inputs (such as non-numeric values or empty fields) are caught before sending the request. This would give the user faster feedback and reduce unnecessary server calls.
2) Use explicit values for the unit dropdowns
The current dropdown relies on the display text for unit values. A better approach would be to define explicit value attributes for each option and map those values directly in the backend. This avoids potential issues caused by formatting differences or capitalization between the UI and server logic
3) Improve handling of external API failures
If the UCUM conversion service fails, the system currently just returns invalid. A better approach would be to detect when the external service fails and return a clearer message. I would also add better logging so these issues are easier to troubleshoot
4) Add a Conversion Preview Feature
Currently the page only tells the user whether the reported value is correct, incorrect, or invalid. An improvement would be to also display the actual converted temperature returned by the UCUM API
5) Validate that the entered values fall within reasonable temperature ranges before performing the conversion.
This can prevent large values being entered, can provide a warning that its falling outside of specific scientific ranges, gives feedback when the input is realistic.
