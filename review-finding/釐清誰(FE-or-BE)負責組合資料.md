<!-- Start: BE 沒有提供某一個欄位的完整內容 -->

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

---

<!-- BE response -->

Hello @TimChou,

I have discussed with @CloverH 

Currently we do not have `avatar` and `role`

And avatar is stored in auth-service if I remered correctly.  -->  Backend 並沒有講明誰(FE or BE)要提供Avator/Role

---

<!-- 釐清誰(FE or BE)要負責提供 -->

@weichen_sun

Thanks for the clarification.

So we’ll need to get avatar from auth-service and join it with audit_log on frontend.

Just to confirm — is this the expected approach, or will backend provide a combined API later?

Thanks!

---

<!-- 如果BE不組資料，要FE組資料必須確認此事 -->

1. 哪一隻API，可以拿到所需的資料。
2. 這隻API只發射一次，還是發射多次?
   - 如果只是一次 -> 前端可做。
   - 如果多次(例如: 每一個row，要trigger API 一次) -> 會有performance issue -> 請PM決定是否要移除這個設計。
3. 考慮pagination 的因素
   - 前端只能拿到當下這個頁面的資料。無法拿到整個資料庫的資料。   
   
---   


   -      