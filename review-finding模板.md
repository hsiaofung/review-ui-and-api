@weichen_sun   

Summary: Mismatch between UI design and API response schema
 
Frontend Review Finding:

User list UI requires:

* avatar
* username
* role

Current API response only provides:

* username

Clarification needed:
1. Is "role" part of user model or available via another endpoint?
2. What is the source of avatar (URL field, separate service, or derived from profile)?

Impact:
UI cannot be fully implemented as per design until data contract is clarified.

Status:
Open Question - pending backend confirmation

Reference:      
API: /log-service/v1/audit_log   
![image](/uploads/3265ccfcde7644a125234d47478eda27/image.png){width=716 height=351}       

UI:    
![image](/uploads/c989625c34aa8eaea8ddf46a09e2a8d6/image.png){width=900 height=480}