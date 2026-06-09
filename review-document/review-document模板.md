---
title: "Log Document"
---

# Audit Log

**Project:** SCC 4.0  
**Module:** Log / Audit Log  
**Type:** Frontend Review  
**Owner:** Tim  
**Status:** Resolved  
**Last Updated:** 2026-06-09

## Open Questions

### Q-001 Navigation View

**Description:**  
Figma/UI Spec/SCC inconsistent.

**Owner:** PM  
**Status:** Pending  
**Dependency:** UI decision required  
**Impact:**  
- Navigation implementation blocked.  
- Audit Log List review can continue.

## Decisions

### D-001 Avatar & Role in Audit Log

**Decision:**  
Avatar and Role removed from Audit Log.

**Reason:**  
Performance concern due to per-row API calls to auth-service.

**Impact:**  
Frontend will NOT render avatars in the Audit Log list.

**Source:**  
PM decision + Clover confirmation

### D-002 Category filter options

**Decision:**  
Category filter options will be implemented as frontend static config:

- Automation
- Device Management
- SCC Configuration
- Security

API only stores categories as string value.

**Source:**  
Clover alignment for SCC 4.0

## API Mapping

**Endpoint:**  
`GET /log-service/v1/audit_log`

**References:**  
- **Swagger**: [http://10.147.34.227:18800/log-service/openapi/v3#/Audit%20Log/get_audit_log_log_service_v1_audit_log_get](http://10.147.34.227:18800/log-service/openapi/v3#/Audit%20Log/get_audit_log_log_service_v1_audit_log_get)  
- **API Document**: [http://scc.pages.supermicro.com/product-project/docs/apis/restful-api/Log/audit-log-log-service-v-1-audit-log-get/](http://scc.pages.supermicro.com/product-project/docs/apis/restful-api/Log/audit-log-log-service-v-1-audit-log-get/)

**UI Component:**  
Audit Log List Figma: [https://www.figma.com/design/lfBdtQs4o8B7cwrvyOpXf3/%E2%91%A2-Log?node-id=4417-116388&t=lXxeOawzYA3SVa1F-0](https://www.figma.com/design/lfBdtQs4o8B7cwrvyOpXf3/%E2%91%A2-Log?node-id=4417-116388&t=lXxeOawzYA3SVa1F-0)

**Mapping:**

| UI Field          | API Field          |
|----------------|--------------------|
| severity       | kedb.severity      |
| timestamp      | eventTime          |
| user           | username           |
| id             | id                 |
| source ip      | ipAddress          |
| category       | kedb.category      |
| subcategory    | kedb.subcategory   |
| device type    | deviceType         |
| error code     | errorCode          |
| message        | kedb.message       |

**Notes:**  
Avatar and Role are not included (removed per UI decision).

## Behavior Layer

### Data Loading
- Data is fetched from `GET /log-service/v1/audit_log` on page load.
- Reload button triggers API re-fetch with current filters.

### Search / Filter
- All table filters (severity, timestamp, user, category, etc.) are applied via backend API query parameters.
- No frontend filtering is performed.
- Each filter change triggers API request.

### Pagination
- Page change triggers API request with `page` + `perPage`.

### Sorting
- Default sort: `timestamp DESC`
- Sorting is triggered via table header interaction.
- Each sort change triggers API request with sort field + order.