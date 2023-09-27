# Incident Report

### 09/23/23
### Time of Outage: 12:00pm 
### Time of Resolution: 3:00pm

# Summary

A new hire was tasked with updating the URL shortener. The new hire committed version 2 of the application to the main branch. Which automatically triggered a build, test, and deploy to the production server, replacing version 1 of the application running on the server. This update caused a 500 internal server error.

# Resolution

* Reverted back to version 2



