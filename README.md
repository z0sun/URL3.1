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

* Rolling back the application to Version 2 highlighted a few issues that I was able to fix.
  - on line 20 of the application.py file, the JSON method was fixed from `json.loads()` to `json.load()` 
<img width="1138" alt="Screen Shot 2023-10-03 at 3 18 44 AM" src="https://github.com/z0sun/URL3.1/assets/135557197/2b1ab781-c380-4185-9031-18c38fca6c84">

* Line 9 of the application.py `@app.routes('/')` was fixed to `@app.route('/')`
<img width="1286" alt="Screen Shot 2023-10-03 at 3 22 53 AM" src="https://github.com/z0sun/URL3.1/assets/135557197/8a452be4-da16-4d3f-9258-4a83b0b7487e">

* Line 6 of the test_app.py was fixed from `assert greeting == "Hi jeff"` to `assert greeting == "Hi jeff "`
<img width="1149" alt="Screen Shot 2023-10-03 at 3 18 27 AM" src="https://github.com/z0sun/URL3.1/assets/135557197/b5bf6b98-7b19-4f3f-9946-abcb3781e3c4">



After these updates to Version 2 were made I then performed a RollBack to Version 1 to make these updates

<img width="534" alt="Screen Shot 2023-10-03 at 3 12 45 AM" src="https://github.com/z0sun/URL3.1/assets/135557197/f1cdc168-5d7d-4faf-a15b-751724d1450d">

# Next Steps

To prevent future incidents: 
- require pull request and approvals to prevent direct commits.
- require permissions for live depolyments.
- add monitoring to build/testing stages to keep track of all changes and affects of those changes earlier in the CI/CD pipeline.



