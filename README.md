# Incident Report

### 09/23/23
### Time of Outage: 12:00pm 
### Time of Resolution: 3:00pm

# Incident Summary

A new hire was tasked with updating the URL shortener. The new hire committed version 2 of the application to the main branch. Which automatically triggered a build, test, and deploy to the production server, replacing version 1 of the application running on the server. This update caused a 500 internal server error. 

# Resolution

* Created a branch of version 2 for trouble shooting the issue.  
* Rolledback to version 1 last working commit, to ensure the SLA is met and we don't exceed alotted downtime.

# Post Incident Troubleshooting

* Version 2 of the application contained two primary issues.
  - on line 20 of the application.py file, the JSON method was fixed from `json.loads()` to `json.load()`
  - the the route method was fixed from `app.routes(/)` to `app.route(/)`

# Next Steps

To prevent future incidents: 
- require pull request and approvals to prevent direct commits.
- require permissions for live depolyments
- add monitoring to build/testing stages to keep track of all changes and affects of those changes earlier in the CI/CD pipeline.



