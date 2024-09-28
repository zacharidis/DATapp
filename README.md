# DATapp
Drugs And Trials (DAT) 

Application Concept: Blind Drug Trials Platform
In a blind trial platform, different entities are involved to ensure data management for clinical trials, patients, drugs, trial administrators, and results. The platform would have users who can manage trials and participants while ensuring that patients are unaware of the details of the drugs they receive.

# Entities/Models
Let's break down the key entities that would be necessary for this application. These entities can be designed to work with a relational database like SQL Server.

User (common for administrators, doctors, and patients)
Fields:
id (Long)
name (String)
email (String)
password (String, hashed)
role (Enum: ADMIN, DOCTOR, PATIENT)
createdAt (Timestamp)
Relations:
One User can be a doctor, patient, or administrator depending on the role.
Doctors create and manage trials, and patients participate in them.
Trial (Represents the drug trial)
Fields:
id (Long)
name (String)
description (String)
startDate (Date)
endDate (Date)
createdBy (Reference to the User, usually a Doctor)
Relations:
A Trial is created and managed by a Doctor (User entity with the role DOCTOR).
A Trial can have multiple patients.
Drug (Represents the drugs used in the trial)
Fields:
id (Long)
name (String)
description (String)
blindCode (String, a code given to anonymize the drug during the trial)
trialId (Reference to the Trial)
Relations:
Each Drug is tied to a specific Trial.
Patient (Represents a patient participating in the trial)
Fields:
id (Long)
userId (Reference to the User table, the role will be PATIENT)
trialId (Reference to the Trial)
assignedDrugId (Reference to the Drug, with anonymized details for the blind trial)
assignedAt (Date when the drug was assigned)
Relations:
A Patient is linked to a Trial and assigned to a Drug.
Result (Represents the outcomes of a trial for a patient)
Fields:
id (Long)
trialId (Reference to the Trial)
patientId (Reference to the Patient)
resultDescription (String, anonymized report)
createdAt (Timestamp)
Relations:
Each Result is tied to a Patient and a Trial.
Feedback (Optional but useful for recording patient feedback)
Fields:
id (Long)
patientId (Reference to the Patient)
trialId (Reference to the Trial)
feedbackText (String)
createdAt (Timestamp)
Relations:
Feedback can be tied to both the Patient and the Trial.

# Relationships Overview:
A User can have different roles (Admin, Doctor, Patient).
A Doctor (User) can manage multiple Trials.
A Trial can have multiple Patients, and each patient is assigned a Drug.
Each Patient in a Trial can submit Feedback and have Results.
Results are submitted anonymously during the blind trial.
