<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>

<h1>Matching - AIC File Project</h1>

<p>This project aims to enhance data quality, automate workflows, and improve accessibility for multiple projects, including Suplari Implementation, P Card, and Travel Analytics. The primary objective is to develop a robust, automated matching framework for AIC files that ensures consistent data across platforms, streamlining workflows and enabling accurate reporting and analysis.</p>

<h2>Key Links and Resources</h2>

<h3>EDP Access and Registration</h3>
<ul>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/GTSD/Registering+and+Getting+access+to+Datasets+in+EDP">Registering and Getting Access to Datasets in EDP - LinkedIn Corporate Wiki</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/GTSD/Registering+and+Getting+access+to+Datasets+in+EDP#RegisteringandGettingaccesstoDatasetsinEDP-WithEDPCLI">Registering and Getting Access with EDP CLI</a></li>
    <li><a href="https://lnkd.visualstudio.com/EPE.CICD/_git/edp-metadata?version=GBmaster">EDP Metadata on Visual Studio</a></li>
    <li><a href="https://microsoft-onmicrosoft-com.access.mcas.ms/aad_login">Requesting Access to EDP Tables</a></li>
</ul>

<h3>EDP Integrations and Connections</h3>
<ul>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/EPEDA/Power+BI+Connecting+to+EDP#PowerBIConnectingtoEDP-Option2:Thisistheregularmethodthatworksforall.">Connecting Power BI to EDP</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/EPEDA/Oracle+to+Hadoop+Filer+based+data+push">Oracle to Hadoop Filer based Data Push</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/GTSD/Registering+and+Getting+access+to+Datasets+in+EDP">Near Real-Time Data for Operational Analytics/Reporting</a></li>
</ul>

<h3>EDP Support and Communication</h3>
<ul>
    <li><a href="https://oncall.prod.linkedin.com/team/team/pe-data-ipa">EDP On Call Dashboard</a></li>
    <li><a href="https://linkedin-randd.slack.com/archives/C0445G24JP8">EDP Slack Channel</a></li>
</ul>

<h3>Finance and Data Platform Resources</h3>
<ul>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/FDP/Finance+Data+Platform+-+FDP">Finance Data Platform - LinkedIn Corporate Wiki</a></li>
    <li><a href="https://microsoft.sharepoint.com/teams/EssbaseandSystems/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FEssbaseandSystems%2FShared%20Documents%2FMasterDataExports&viewid=8dc03049%2Dcb0e%2D4e38%2D8714%2D2075dc50c803D">Master Data Exports</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/FDP/Travel+BCD+-+Finance+Data+Platform">Travel BCD - Finance Data Platform</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/IST/Revenue+Analytics+-+Ada+Ma">Revenue Analytics - Ada Ma</a></li>
</ul>

<h3>Access Requests and Permissions</h3>
<ul>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/IST/How+to+Request+SGP-ENG+Group+Memberships+in+LIDM">Requesting SGP-ENG Group Memberships</a></li>
    <li><a href="https://jira.linkedin.com/browse/SYSOPS-146199">Access to Oracle EBS Database - LinkedIn JIRA</a></li>
    <li><a href="https://iwww.corp.linkedin.com/wiki/cf/display/IST/EBS+Instances">EBS Instances - Information Services & Technology</a></li>
</ul>

<h2>Project Structure</h2>
<ul>
    <li><strong>docs/</strong> - Documentation files including data dictionary, architecture, and analysis notes.</li>
    <li><strong>config/</strong> - Configuration files for database connections, environment settings, and mapping schemas.</li>
    <li><strong>sql/</strong> - SQL scripts categorized into raw data extraction, transformations, aggregations, and matching logic.</li>
    <li><strong>etl/</strong> - ETL pipeline code with modular functions for data normalization, matching, enrichment, and validation.</li>
    <li><strong>scripts/</strong> - Utility scripts for validating matches, checking data quality, and generating reports.</li>
    <li><strong>data_samples/</strong> - Sample data files (sanitized) for testing ETL processes, including raw and processed data.</li>
</ul>

<h2>Data Tables and Columns</h2>
<p>The following tables and columns are key to the Matching - AIC File project:</p>
<table border="1" cellpadding="10" cellspacing="0">
    <thead>
        <tr>
            <th>Table Name</th>
            <th>Key Columns</th>
        </tr>
    </thead>
    <tbody>
        <tr><td>GL_DAILY_RATES</td><td>Conversion Date, From Currency, To Currency, Conversion Rate</td></tr>
        <tr><td>HR_OPERATING_UNITS</td><td>Organization ID, Name, Location</td></tr>
        <tr><td>HZ_CUST_ACCOUNTS</td><td>Account Number, Customer ID, Customer Name</td></tr>
        <!-- More rows as needed -->
    </tbody>
</table>

<h2>Getting Started</h2>
<ol>
    <li>Clone the repository.</li>
    <li>Install required packages by running <code>pip install -r requirements.txt</code>.</li>
    <li>Set up database connections by configuring <code>db_connections.yaml</code> in the <code>config/</code> folder.</li>
    <li>Prepare sample data in the <code>data_samples/</code> folder for initial testing.</li>
</ol>

<h2>Running the ETL Pipeline</h2>
<p>The main ETL pipeline is located in <code>etl/main_etl_pipeline.py</code>. You can run the entire ETL process or execute individual modules as needed:</p>
<pre><code>python etl/main_etl_pipeline.py</code></pre>

<h2>Scripts</h2>
<ul>
    <li><strong>validate_matches.py</strong> - Checks matching accuracy and provides metrics on match rates.</li>
    <li><strong>check_data_quality.py</strong> - Runs data quality checks to identify inconsistencies.</li>
    <li><strong>generate_reports.py</strong> - Generates reports on the matching process and progress.</li>
</ul>

<h2>Key Documentation</h2>
<ul>
    <li><strong>data_dictionary.md</strong> - Detailed documentation of tables, fields, and relationships.</li>
    <li><strong>architecture.md</strong> - High-level overview of data architecture and system integration.</li>
    <li><strong>troubleshooting.md</strong> - Common issues and solutions for data and ETL challenges.</li>
</ul>

<h2>Contributing</h2>
<p>For contributions, please adhere to the following guidelines:</p>
<ol>
    <li>Use branches for specific features or modules, and provide descriptive names (e.g., <code>feature/fuzzy_matching</code>).</li>
    <li>Commit regularly with clear messages describing changes made.</li>
    <li>Document any new functions or scripts added to the repository.</li>
</ol>

<h2>Contact</h2>
<p>For any questions or further assistance, please reach out to the project lead, Scott Morgan.</p>

</body>
</html>
