# Security Applied Field Engineering
# SAFE: Strong Authentication Flow Evaluator


-----

## Overview

The **Strong Authentication Flow Evaluator (SAFE)** is a Streamlit-based application designed to assist Snowflake Account Administrators in evaluating the authentication methods used within their Snowflake accounts. Developed and maintained by the Snowflake Security Applied Field Engineering (SAFE) team, this application helps administrators ensure their current account configurations comply with upcoming Snowflake policy changes. These changes deprecate single-factor password sign-ins and limit allowed authentication methods based on user **TYPE**.

SAFE aggregates findings from `LOGIN_HISTORY`, configured authentication options, and other account metadata. This allows administrators to make informed decisions regarding a user's object **TYPE** and its required authentication methods. The **ACTIONS** section within the application empowers administrators to **SET** the appropriate **USER TYPE** and **UNSET PASSWORDS** where necessary, accelerating the creation of authentication policies and promoting adherence to best practices for user object management in Snowflake.

The tool acts as an interactive wrapper for the guidance outlined in:

  * [Snowflake Perimeter Security Guidance](https://www.google.com/search?q=https://docs.snowflake.com/en/user-guide/admin-security-perimeter)
  * [Password Eradication (SAFE app)](https://www.google.com/search?q=https://medium.com/snowflake/password-eradication-a-secure-authentication-best-practice-for-snowflake-9e1e0a2f1a66)
  * [Snowflake SAFE Medium List](https://www.google.com/search?q=https://medium.com/snowflake/tagged/safe)


![image](https://github.com/user-attachments/assets/a93a62b3-daec-4783-94e7-23276e1c0399)

-----

## Features

The SAFE App UI enables discovery and seamless remediation by providing the following features:

  * **Identifies static credentials** in Snowflake for eradication (unset) or enrollment in MFA (Passkeys, TOTP, Duo).
  * **Discovers client authentication patterns** to help set the appropriate user type.
  * **Highlights non-human identities** (machine-to-machine flows) that need to adopt OAuth, Workload Identity Federation, Key Pair, or Programmatic Access tokens for the **SERVICE** user type.
  * **Provides a clear dashboard** of authentication factors across your Snowflake environment.
  * **Lightweight and quick to deploy** using Streamlit.
  * **Expected compute and cost estimate** details will be provided within the application or documentation.

-----

## Use Cases

As Snowflake continues to enforce modern authentication requirements, SAFE helps shorten the time to value by:

  * Running checks against `login_history` and `users` views.
  * Setting the appropriate user type (**HUMAN**, **SERVICE**, **LEGACY\_SERVICE**).
  * Flagging non-compliant authentication flows.
  * Facilitating discovery to plan remediation or automation updates to authentication patterns.
  * Eradicating static credentials where applicable.

  * ![image](https://github.com/user-attachments/assets/6b8a37e6-87e8-4a3f-b1a0-807142445368)


-----

## Roadmap

  * **CIDR discovery** for Account and User Level Network Policy discovery, enforcement, and least privilege measurement.

-----

## Contributions & Support

For contributions or support, please contact: `safe@snowflake.com`

-----

## Authors & Acknowledgements

A special thank you to the maintainers:

  * Vladimir Timofeenko
  * Peter Horrigan

And the Snowflake Security Applied Field Engineering Team - Americas:

  * Ryan O’Connell
  * Mike Mitrowski
  * Eugene Choi
  * Nick Nieves
  * Amir Durrani
  * Sean Cooper
  * Jake Berkowsky
  * Matt Barreiro

-----

## Requirements

To run the SAFE application, you will need:

  * **Python 3.8+**
  * **Snowflake account** with `ACCOUNTADMIN` or sufficient privileges to query `login_history` and `users`.
  * [**Snowflake Python Connector**](https://docs.snowflake.com/en/developer-guide/python-connector)
  * [**Streamlit**](https://streamlit.io/)
  * A `.env` file or secrets manager for credentials.

-----

## Installation

This project is designed to run as a **Streamlit Native App** inside your Snowflake account.

### Step 1: Prepare Your Snowflake Environment

Ensure you have the following:

  * A role with `CREATE APPLICATION` and `CREATE DATABASE` privileges.
  * Access to a working Snowflake warehouse.
  * `ACCOUNTADMIN` or a role with privileges to read from `SNOWFLAKE.ACCOUNT_USAGE` views (e.g., `login_history`, `users`).

### Step 2: Clone the Repo

```bash
git clone https://github.com/your-org/safe.git
cd safe
```

### Step 3: Deploy the Streamlit Native App

```sql
-- 1. Create a database for your Streamlit app (optional)
CREATE DATABASE SAFE_APP_DB;

-- 2. Create or use a schema
USE SCHEMA SAFE_APP_DB.PUBLIC;

-- 3. Create the Streamlit application
CREATE OR REPLACE STREAMLIT SAFE_APP
FROM '@your_stage/safe'
MAIN_FILE = '/app.py';
```

### Step 4: Grant Usage

```sql
GRANT USAGE ON STREAMLIT SAFE_APP TO ROLE YOUR_ROLE;
```

-----

**Important Disclaimer:**

Customers should leverage internal policies and standards in addition to Snowflake guidance, including Snowflake’s Trust Center or the Cloud Security Posture Management (CSPM) tool of their choice, to guide any remediation effort. This resource is not a substitute for a thorough, services-led engagement, nor does it supersede any other obligations you may have to Snowflake, your organization, your outside regulators, or other bodies to which you owe compliance or conformance.

-----

## License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE).

-----
