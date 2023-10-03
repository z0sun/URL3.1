# Incident Report

### 09/23/23
### Time of Outage: 12:00pm 
### Time of Resolution: 3:00pm

# Incident Summary

A new hire was tasked with updating the URL shortener. The new hire committed version 2 of the application to the main branch. Which automatically triggered a build, test, and deploy to the production server, replacing version 1 of the application running on the server. This update caused a 500 internal server error. 

# Resolution

* To meet the SLA aggreement and avoid downtime the best resolution to this issue was to Rollback to version 1 of the application to ensure availability. Below were the rollback steps:
  ```
    git checkout 4707109
    git switch main
    git checkout 4707109 .
    git log --oneline
    git status
    git add
    git add .
    git commit -m "Rollback to Version 1 fom 2"
    git push
  ```
* Next, I created a branch of version 2 for troubleshooting the issue.  

# Post Incident Troubleshooting

* Rolling back the application to Version 2 highlighted two primary issues.
  - on line 20 of the application.py file, the JSON method was fixed from `json.loads()` to `json.load()` 


# Next Steps

To prevent future incidents: 
- require pull request and approvals to prevent direct commits.
- require permissions for live depolyments
- add monitoring to build/testing stages to keep track of all changes and affects of those changes earlier in the CI/CD pipeline.



