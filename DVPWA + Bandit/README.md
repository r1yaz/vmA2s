# DVPWA + Bandit

Run bandit SAST scans over the dvpwa (Damn Vulnerable Python Web Application) repository using GitLab CI.

## Code

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

### Next steps
1. Achieve the same using GitHub Actions
2. Achieve the same using CircleCI

