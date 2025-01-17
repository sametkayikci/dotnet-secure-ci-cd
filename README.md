# .NET Secure CI/CD Pipeline

This repository provides a sample CI/CD pipeline configuration for .NET projects, focusing on security and reliability throughout the development lifecycle.

## Features

- **Build**: Builds the .NET project using the latest .NET SDK (v8.0).
- **Security Scans**:
  - **SAST**: Static Application Security Testing to detect code vulnerabilities.
  - **Dependency Scanning**: Checks for vulnerabilities in third-party dependencies.
  - **Secret Detection**: Identifies hardcoded secrets in the codebase.
  - **IaC SAST**: Scans Infrastructure as Code files using KICS.
- **Security Reports**: Validates security scan results, blocking the pipeline for high or critical vulnerabilities.
- **Deployment Protection**: Prevents merging to the main branch if security issues are detected.

## Stages

1. **Build**
   - Restores and builds the .NET project in Release configuration.

2. **Security-Scan**
   - Runs SAST, Dependency Scanning, and IaC scans to identify security vulnerabilities.

3. **Secrets**
   - Detects hardcoded secrets in the codebase.

4. **Security-Report**
   - Aggregates and validates security findings across all scans.

5. **Test**
   - Placeholder stage for integrating unit or integration tests.

6. **Deploy**
   - Protects the main branch by blocking merges if critical issues are present.

## Configuration Details

### Pipeline Variables
- `SAST_FAIL_ON_SEVERITY`: Blocks the pipeline for specified severity levels (e.g., `high`).
- `SECURE_LOG_LEVEL`: Debug level for detailed scan logs.

### Tools Used
- **GitLab Templates** for SAST, Dependency Scanning, and Secret Detection.
- **KICS** for IaC SAST.

### Artifacts
- Security scan results are saved as JSON reports for further analysis:
  - `gl-sast-report.json`
  - `gl-dependency-scanning-report.json`
  - `gl-secret-detection-report.json`
  - `kics_sast_report.json`

## How It Works

1. The pipeline starts with the `build` stage, ensuring the project compiles successfully.
2. Security scans are executed in the `security-scan` stage, generating reports.
3. Secret detection runs in the `secrets` stage to identify hardcoded credentials.
4. The `security-report` stage validates all scan results and blocks the pipeline if high or critical vulnerabilities are detected.
5. The `deploy` stage prevents merging to the `main` branch if unresolved security issues exist.

## Usage

1. Clone this repository.
2. Customize the pipeline variables and scripts as needed for your project.
3. Push the `.gitlab-ci.yml` file to your GitLab repository.

## Contributing

Feel free to submit issues or pull requests to improve this pipeline configuration.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
