# Introduction:
This project is heavily inspired by the [OWASP Web Security Testing Guide (WSTG)](https://owasp.github.io/www-project-web-security-testing-guide/), and their amazing work in standardizing and documenting web security best practices.

## Purpose and Scope
In short, this framework provides a central resource for testing and securing Azure DevOps environments. We aim to map and document attack vectors and areas of risk so that defenders can approach securing their environments in a structured and repeatable manner.

In terms of scope, the framework deals only with Azure DevOps; other factors like software supply chains and security testing of source code are not a part of the framework. The inclusion of scanning (SAST, DAST, SCA) in CI/CD processes is included, but not the security of the underlying software itself. So, to summarize, the scope is the platform and configuration of platform-specific elements, not the software security itself; for this, please refer to resources such as the [https://owasp.github.io/www-project-web-security-testing-guide/](OWASP WSTG).

## Why Testing of Your DevOps Matters
DevOps setups stand as a central part of the modern software development lifecycle. This is due to the functionality needed to both manage and deliver software. These systems often store critical data such as source code and also integrate into critical business processes; this often also means that they have high privileges and access to key infrastructure assets. Thus, if these are compromised, this can lead to critical business impact and potentially compromise additional related services and assets.

A key case illustrating how a compromise of a CI/CD platform can lead to severe business impact is the case of the [Novo Nordisk compromise in 2026](https://www.enterprisesoftproducts.com/blog/20260618NovoNordiskHack.html), where attackers gained read access to the organization's GitHub. This access was then used to compromise key business secrets like drug formulas and processes. Attackers were furthermore able to compromise related assets like other cloud providers, AI training data and weights in the organization's Hugging Face tenant, and much more.

## Who Should Use This Guide
The Ado-STG is designed for:
- Penetration testers and security professionals who conduct ADO security reviews.
- In-house security professionals in charge of securing ADO setups.
- Developers and infrastructure professionals working in ADO.

Secondary audiences include management and governance specialists in charge of defining and implementing security requirements for their DevOps setup.

## How is This Gudie Structured
The Ado-STG is structured as follows:
- [Azure DevOps - Security Testing Guide (Ado-STG)]([/](https://www.enterprisesoftproducts.com/)resources/azuredevops/home.html) - This page contains the introduction to the project, explains the framework, and sets the context for the use of the framework</li>
- Azure DevOps - Security Testing Guide Categories - Provides concrete, how-to-test procedures for each major building block of ADO (e.g., pipeline injection, organization setup, service connections, etc.)

Readers new to security testing should start here and then progress through each of the categories and gain a general understanding of the structure of the individual tests. Then, when testing, follow the how-tos and approach testing in a structured manner, remembering to keep good notes and track progress throughout the entire process.


# Terms of use
## License and Attribution

The Ado-STG is released under the "CC BY-SA 4.0" license. In essence, this means that anyone is free to share and modify the project. You are, however, required to attribute any use of the project to Enterprise Softproducts; you are required to use the same license for any projects using this content; and lastly, you may not add additional restrictions to any derivative works.

[![Creative Commons License](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/ "CC BY-SA 4.0")

If you are a consultant and using this framework for your assessments, please also reference Enterprise Softproducts and this framework.

## How To Reference Ado-STG Scenarios
Each scenario has an identifier in the format AdoSTG-<category>-<number>, where 'category' is a 2-3 character uppercase string that identifies the type of test or weakness, and 'number' is a zero-padded numeric value from 01 to 99. For example: AdoSTG-SC-02 is the second Service Connection test.
