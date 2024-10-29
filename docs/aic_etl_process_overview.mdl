<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AIC ETL Documentation</title>
</head>
<body>

<h1>AIC ETL Documentation</h1>

<p>This document outlines the ETL process for the AIC project, detailing the key steps involved in data import, transformation, and publishing to the final table. Each section highlights critical tasks, from data merging to supplier classification, as well as SQL snippets where applicable.</p>

<h2>1. Data Import and Initial Processing</h2>
<p>Data from PCard and Spend datasets are imported into Omniscope. The data from both sources is appended, and then formatted by renaming and removing unnecessary fields. Finally, it is merged with Coupa data by matching on PO Number and Supplier Name to bring in the Purchase ID from the Coupa dataset.</p>

<pre><code>
// Example SQL: Initial Data Import and Merge
SELECT * 
FROM pcard_data 
INNER JOIN spend_data ON pcard_data.PO_Number = spend_data.PO_Number;
</code></pre>

<h2>2. Data Normalization and Enrichment</h2>
<ul>
    <li><strong>Supplier Name Normalization:</strong> Normalizes supplier names using the <code>kbNormalisation</code> table. Unmatched suppliers are set as "UNKNOWN SUPPLIER".</li>
    <li><strong>Region and Country Assignment:</strong> Updates region and country based on <code>luCompanyRegions</code>.</li>
    <li><strong>Supplier Type Update:</strong> Sets the type to "PCARD" for system type "PCARD" entries.</li>
    <li><strong>Payment Terms:</strong> Updates payment terms using the <code>kbPaymentTerms</code> table.</li>
</ul>

<pre><code>
// Example SQL: Supplier Normalization
UPDATE tblRefresh
SET Normalized_Supplier = kbNormalisation.Normalized_Supplier
FROM tblRefresh
INNER JOIN kbNormalisation ON tblRefresh.Supplier_Name = kbNormalisation.Supplier_Name;
</code></pre>

<h2>3. Classification and Categorization</h2>
<p>Classification data is updated in <code>tblRefresh</code> using various lookup tables for detailed categorization. This step involves setting categories like Category 1, Category 2, and Category 3 based on supplier names, supplier numbers, and other conditions.</p>

<pre><code>
// Example SQL: Classification Update
UPDATE tblRefresh
SET Category_1 = luCategoryMap.Category_1,
    Category_2 = luCategoryMap.Category_2,
    Category_3 = luCategoryMap.Category_3
FROM tblRefresh
INNER JOIN luCategoryMap ON tblRefresh.Supplier_Name = luCategoryMap.Supplier_Name;
</code></pre>

<h2>4. Contract and Financial Information Update</h2>
<ul>
    <li><strong>Contract Information:</strong> Updates contract details in <code>tblRefresh</code> by pulling values from <code>luApptusContracts</code>.</li>
    <li><strong>Financial Year and Period:</strong> Sets financial year, quarter, and period using <code>luFinancialYear</code>.</li>
</ul>

<pre><code>
// Example SQL: Contract Update
UPDATE tblRefresh
SET Contract_Number = luApptusContracts.Contract_Number
FROM tblRefresh
INNER JOIN luApptusContracts ON tblRefresh.PO_Number = luApptusContracts.PO_Number;
</code></pre>

<h2>5. Preferred Supplier Identification</h2>
<p>Identifies preferred suppliers by matching with the <code>luPreferredSuppliersList</code>. If no match is found, the field is set to "No".</p>

<pre><code>
// Example SQL: Preferred Supplier Flag
UPDATE tblRefresh
SET Preferred_Supplier = CASE WHEN luPreferredSuppliersList.Supplier_Name IS NOT NULL THEN 'Yes' ELSE 'No' END
FROM tblRefresh
LEFT JOIN luPreferredSuppliersList ON tblRefresh.Supplier_Name = luPreferredSuppliersList.Supplier_Name;
</code></pre>

<h2>6. Diversity and Risk Indicators</h2>
<ul>
    <li><strong>Diversity:</strong> Updates diversity information based on tables like <code>luDiversity1</code>, <code>luDiversity2</code>, and <code>luDiversity3</code>.</li>
    <li><strong>Risk Factor:</strong> Sets risk indicators using data from <code>luSSANumbers</code>.</li>
</ul>

<h2>7. Invoice and Vendor Spend Calculations</h2>
<p>Calculates invoice totals and spend ranges per vendor and updates <code>tblRefresh</code> with labels to indicate ranges and classifications for spend analysis.</p>

<pre><code>
// Example SQL: Spend Calculation
SELECT Supplier_Name, SUM(Spend) AS Total_Spend
FROM tblRefresh
GROUP BY Supplier_Name;
</code></pre>

<h2>8. Final Publishing and QA</h2>
<p>After completing the transformations and classifications, the data is sent to the QA team for validation. Any necessary adjustments are made based on feedback, and then the data is published to Looker for reporting and analysis.</p>

<h2>9. Special Classification Rules</h2>
<ul>
    <li><strong>American Express and LinkedIn Suppliers:</strong> Set to "Non-Addressable" for specific classifications.</li>
    <li><strong>Category Assignments:</strong> Updates categories for unique suppliers based on internal business rules.</li>
</ul>

<pre><code>
// Example SQL: Non-Addressable Classification
UPDATE tblRefresh
SET Addressable = 'Non-Addressable'
WHERE Supplier_Name IN ('AMERICAN EXPRESS', 'LINKEDIN EMPLOYEE');
</code></pre>

<h2>10. Additional Details and Table Definitions</h2>
<p>Refer to the data dictionary for detailed table and field definitions, located in the <code>docs/</code> folder of this repository. This document includes an overview of the primary tables such as <code>tblRefresh</code>, <code>kbNormalisation</code>, <code>luCategoryMap</code>, and others.</p>

</body>
</html>
