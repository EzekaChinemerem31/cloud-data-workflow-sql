# cloud-data-workflow-sql
Technical implementation of a cloud native data synchronization workflow. Features SQL-based data management, system troubleshooting queries and IAM security logic.
-- SQL Script: Managing Medical Imaging Data Workflows in AWS
-- Purpose: Database management for PACS/DICOM records synced to AWS S3

-- 1. Create a table to track X-ray scans and their AWS Cloud sync status
CREATE TABLE Radiology_Workflows (
    ScanID INT PRIMARY KEY,
    Patient_Name VARCHAR(100),
    Modality_Vendor VARCHAR(50), -- Siemens, Philips, Carestream, etc.
    Modality_Type VARCHAR(20),   -- XR, CT, MRI
    Sync_Status VARCHAR(20),     -- Pending, Completed, Error
    AWS_S3_Bucket VARCHAR(50)    -- The AWS storage location
);

-- 2. Insert records based on clinical experience
INSERT INTO Radiology_Workflows VALUES (1, 'Patient_A', 'Siemens', 'XR', 'Completed', 'medical-images-s3-01');
INSERT INTO Radiology_Workflows VALUES (2, 'Patient_B', 'Philips', 'CT', 'Pending', 'medical-images-s3-01');
INSERT INTO Radiology_Workflows VALUES (3, 'Patient_C', 'Carestream', 'XR', 'Error', 'medical-images-s3-02');

-- 3. Troubleshooting Query: Find all Philips scans that failed to sync to AWS
SELECT Patient_Name, Modality_Vendor, Sync_Status 
FROM Radiology_Workflows 
WHERE Modality_Vendor = 'Philips' AND Sync_Status != 'Completed';
