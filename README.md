# COBOL Check Automation

A CI/CD pipeline that automates COBOL unit testing and deployment to a live z/OS mainframe, using GitHub Actions, Zowe CLI, and Cobol Check.

## What this does

On every push to `main`, this pipeline:
1. Installs Java, Node.js, Zowe CLI, and GnuCOBOL on a GitHub-hosted runner
2. Runs [Cobol Check](https://github.com/openmainframeproject/cobol-check) unit tests against COBOL programs
3. Uploads the compiled test programs and JCL files directly to a real z/OS mainframe via Zowe CLI
4. Leaves the JCL ready to compile and execute on the mainframe (via IBM Enterprise COBOL / IGYWCL)

**Flow:**

GitHub push → GitHub Actions → Zowe CLI → z/OS Mainframe

Cobol Check + GnuCOBOL (unit tests run in CI)

## Programs included

| Program  | Description                                  |
|----------|-----------------------------------------------|
| NUMBERS  | Sample numeric relations/comparison program   |
| EMPPAY   | Employee weekly/monthly payment calculator    |
| DEPTPAY  | Department average salary calculator          |

Each program has:
- COBOL source (`cobol-check/src/main/cobol/`)
- A Cobol Check test suite (`cobol-check/src/test/cobol/`)
- A JCL file to compile and run it on the mainframe (repo root)

## Why this project

Most mainframe environments still rely on manual JCL submission and ad hoc testing. This project demonstrates:
- Writing and running **unit tests for COBOL** using a TDD-style approach
- Automating deployment from a modern CI/CD tool (GitHub Actions) to a mainframe via **Zowe CLI**
- Debugging real integration issues across environments — COBOL fixed-format column rules, case-sensitive USS paths, Zowe authentication, JCL member references, and GnuCOBOL vs. IBM Enterprise COBOL compiler differences

## Tech stack

`GitHub Actions` · `Zowe CLI` · `Cobol Check` · `GnuCOBOL` · `IBM Enterprise COBOL` · `JCL` · `z/OS`

## Setup

Requires:
- A Zowe CLI profile configured for your z/OSMF connection
- `ZOWE_USERNAME` and `ZOWE_PASSWORD` set as GitHub repository secrets

See `.github/workflows/main.yml` for the full pipeline configuration.
