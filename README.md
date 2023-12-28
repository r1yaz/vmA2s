# vmA2s

> DevSecOps projects/code which I've built and am in the process of open sourcing it. Releasing every 2-3 days.

## DVPWA + Bandit

[![security: bandit](https://img.shields.io/badge/security-bandit-yellow.svg)](https://github.com/PyCQA/bandit)

Run bandit SAST scans over the dvpwa (Damn Vulnerable Python Web Application) repository using GitLab CI.

#update things here regarding the 3 screenshots you added (with ref links)
start a new project


### Code

```yaml
stages: #denotes the stages in the pipeline. we need only one stage.
  - bandit_scan #since we're running a bandit scan, it's bandit_scan :)

build-job:
  stage: bandit_scan #which stage does this job belong to?
  image: python:3.6 #what image are we cloning to run this?
  script:
    - git clone https://github.com/anxolerd/dvpwa #clone DVPWA
    - cd dvpwa #cd into the folder
    - pip3 install bandit #install the bandit package
    # Run bandit with verbose (-v), recursive (-r) so that it scans all the subdirectories too, pass the path to dvpwa, output format as json (-f), and we want to store the output file as result.json (-o)
    - bandit -v -r /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa -f json -o /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa/result.json
  artifacts: #To keep the generated output result.json as an artifact
    when: always #ensure that this artifact is present even if the build fails
    paths: #where to store the artifact
      - /builds/sample_devsecops/damnvulnerablepythonapp/dvpwa/result.json
```

Clean code present in [.gitlab-ci.yml](https://github.com/r1yaz/vmA2s/blob/main/DVPWA%20+%20Bandit/.gitlab-ci.yml)

### Results

Update the YAML CI/CD Code into a repository as the .gitlab-ci.yml file.

![.gitlab-ci.yml](https://github.com/r1yaz/vmA2s/blob/main/Images/dvpwa_bandit_1.png)

Auto-trigger the pipeline when a commit is made to the repository and a valid .gitlab-ci.yml file is present. As indicated, Artifact is generated and uploaded.

![.gitlab-ci.yml](https://github.com/r1yaz/vmA2s/blob/main/Images/dvpwa_bandit_2.png)

Artifact contains bandit scan reports of the Damn Vulnerable Python Web Application as highlighted below.

![.gitlab-ci.yml](https://github.com/r1yaz/vmA2s/blob/main/Images/dvpwa_bandit_3.png)



