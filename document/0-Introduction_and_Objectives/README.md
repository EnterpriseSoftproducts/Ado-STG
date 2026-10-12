# Introduction and Objectives

This section describes the Enterprise Softproducts Azure DevOps security testing methodology and explains how to test for evidence of vulnerabilities within the application due to deficiencies with identified security controls.

## What is Azure DevOps Security Testing?

A security test is a method of evaluating the security of a computer system or network by methodically validating and verifying the effectiveness of application security controls. A test of an Azure DevOps setup focuses only on evaluating the security of an Azure DevOps setup, by this we only mean parts specific to the platform such as project, repositories, and pipelines. We are not evaluating the code hosted on the platform. The process involves an active analysis of the application for any weaknesses, technical flaws, or vulnerabilities. Any security issues that are found will be presented to the system owner, together with an assessment of the impact, a proposal for mitigation or a technical solution.

## What is a Vulnerability?

A vulnerability is a flaw or weakness in a system's design, implementation, operation or management that could be exploited to compromise the system's security objectives.

## What is a Threat?

A threat is anything (a malicious external attacker, an internal user, a system instability, etc.) that may harm the assets owned by an application (resources of value, such as the data in a database or in the file system) by exploiting a vulnerability.

## What is a Test?

A test is an action to demonstrate that an application meets the security requirements of its stakeholders.

## The Approach in Writing this Guide

Enterprise Softproducts approach is open and collective:

- Open: every security expert can participate with their experience in the project. Everything is free.
- Collaborative: additions, comments, and changes from the users and community are welcomed and encouraged.

This approach tends to result in a defined Testing Methodology that will be:

- Consistent
- Reproducible
- Rigorous
- Under quality control

The problems to be addressed are fully documented and tested. It is important to use various methods to test all the known vulnerabilities and document all the security test activities.

## What Is the Enterprise Softproducts Testing Methodology?

Security testing will never be an exact science where a complete list of all possible issues that should be tested can be defined. In fact, security testing is only one of the several suitable techniques for testing the security of web applications under certain circumstances. The goal of this project is to collect all the possible testing techniques, explain these techniques, and keep the guide updated. 

The testing model consists of:

- Tester: Who performs the testing activities
- Tools and methodology: The core of this Testing Guide project
- Application: The Azure DevOps environment
