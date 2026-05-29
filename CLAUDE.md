# YMS Improvements v4 — Project Context

**Project:** [BR FRF] YMS Improvements v4
**Owner:** Camila Braz (camila.braz@shopee.com) — Product Manager, Shopee BR
**Role:** You are a product manager at Shopee focused on developing solutions, documenting them for the development team, serving both operations and development.

---

## What This Project Is

A Feature Requirements File (FRF) documenting improvements to the YMS (Yard Management System) for Shopee BR. The main document is `[BR FRF] YMS Improvements v4 atualizado.docx`.

The FRF is structured as:
1. Background
2. Objectives
3. Business Impact
4. Business Requirements (main working area)
5. Scenarios
6. Data Information
7. Expected Delivery Date

---

## Business Requirements Structure

### 4.1 Automatic Assignment
- **4.1.1 Dock Attributes** — priority criteria for dock assignment
- **4.1.2 Change logic** — assignment logic changes

### 4.2 Entry Site Configuration
- **4.2.1 Remove dock limit**
- **4.2.2 Add geofence** — zone management, station geofence tag
- **4.2.3 New entry site config** — Vehicle Capacity Control tab in SPX Admin
  - 4.2.3.1–4.2.3.4 subsections (vacancy cascade, driver experience)

### 4.3 Notifications Improvements (Gate Queue Control)
- **4.3.1 Phased Notifications** — Gate Queue Control feature
  - 4.3.1.1 Configuration parameters
  - 4.3.1.2 Gate capacity evaluation
  - 4.3.1.3 Driver notification and confirmation
  - 4.3.1.4 Geofence tracking and meter release
- **4.3.2 End Process Notifications** — dock completion notifications
  - 4.3.2.1 Configuration parameters
  - 4.3.2.2 Messages, triggers and behavior

### 4.4 Queue List Visibility (pending)

### 6. Data Information
- Data tables and logs for Gate Queue Control (to be written)

---

## Key Technical Concepts

### Gate Queue Control (4.3.1)
- Controls physical gate area (portaria) capacity in meters
- Formula: `occupied_meters + next_vehicle_length ≤ gate_capacity_m`
- `occupied_meters` = sum of vehicle lengths of drivers with Entry Tag = Portaria + Queue Status = Assigned
- Gate check triggers ONLY for external drivers (external → internal transition)
- Meters reserved ONLY after driver read-confirms notification
- On Hold = retry limit reached, meters released, manual ops intervention required

**Queue Status values:** Pending / Assigned / On Hold
**Entry Tag:** always represents the next destination of the driver
- Waiting in external lot → Entry Tag = external lot name
- Notification sent (modal active) → Entry Tag = Portaria (hidden behind modal)
- Confirmed → Entry Tag = internal lot / dock (final destination)
- On Hold → Entry Tag reverts to external lot

**Configuration (SPX Admin):**
Path: FMS > Station Management > Queue & Dock Management > Vehicle Capacity Control
- Gate Area Geofence (must be within Station Geofence, tagged "Portaria" in Zone Management)
- Gate Queue Capacity (m)
- Confirmation Timeout (min)
- Max Travel Time (min)
- Retry Limit (attempts)
- Validation at Save, not at toggle activation

**Portaria Tag:** Created in Zone Management via "More ▾" dropdown → "◉ Tag as Portaria" — same pattern as Station Geofence tag.

**Vehicle length:** sourced from Fleet Management > Vehicle Type Config > Modify > Length (cm). System converts cm to meters.

### End Process Notifications (4.3.2)
4 independent notifications, all optional, configurable per task type per station:

| # | Name | Recipient | Trigger |
|---|---|---|---|
| 1 | Progress Alert | Current driver at dock | X₁% of task orders processed |
| 2 | End Process | Current driver at dock | Task fully completed |
| 3 | Pre-Call | Next driver (position 1) | X₂% of task orders processed |
| 4 | Effective Call | Next driver (cascade) | Dock freed |

- X₁% and X₂% are independent, configurable per task type
- Task types: LM (Assignment Task/AT), FM (Pick Up Task), LH (Linehaul Task)
- Task-specific statuses that indicate completion: **TBD** (to be aligned with LH/FM/LM teams)
- Re-send: operator can manually re-send Notification 2 via "Inform Driver" button in Queue List
- Queue List gets two new columns: Task ID + Task Status (for LH and AS tasks)

**Configuration path:** FMS > Station Management > Queue & Dock Management > Queue & Dock Configurations > Process Notifications tab
- Same breakdown as Automatic Queue Registration: LH-Inbound, LH-Outbound, LH-Inbound & Outbound, FM-Inbound, Delivery-Outbound

---

## Mockup Files

### 4.1-automatic-assignment/
- `4114-examples-table.html` — 4.1.1.4 examples (full)
- `4114-gdocs-table.html` — 4.1.1.4 examples (GDoc format)
- `4122-examples-table.html` — 4.1.2.2 examples (full)
- `4122-gdocs-table.html` — 4.1.2.2 examples (GDoc format)
- `assignment-priority-flow.html` — assignment priority flow diagram
- `automatic-dock-assign-fixed.html` — automatic dock assignment mockup

### 4.2-entry-site-config/
- `entry-site-config-animated.html` ← **FINAL animated version** (auto-plays demo)
- `entry-site-config-interactive.html` ← **FINAL interactive version** (manual use)
- `entry-site-geofence-interactive.html` — geofence config mockup
- `zone-management-interactive.html` — Zone Management with Station Geofence tag
- `entry-site-assignment-flow.html` — entry site assignment flow
- `vacancy-cascade-flow.html` — vacancy cascade flow
- `sta-check-flow.html` — STA check flow
- `early-arrival-monitoring-flow.html` — early arrival flow
- `geofence-arrival-flow.html` / `.png` — geofence arrival flow

### 4.3-gate-queue-control/
- `gate-queue-control-mockup.html` — SPX Admin: Vehicle Capacity Control tab (interactive, includes Gate Queue Control section + Zone Management)
- `notification-flow-4.3.html` — 4.3.1 phased notification flow diagram (SVG)
- `driver-gate-queue-mockup.html` — Driver App: Queue Status (3 states: Waiting / Notification / On Hold)
- `zone-management-portaria-tag.html` — Zone Management with Portaria tag (same pattern as Station tag)

### 4.3.2-end-process-notifications/
- `end-process-notifications-flow.html` — Before & After + full 4-notification flow diagram
- `process-notifications-config-mockup.html` — SPX Admin: Process Notifications tab config
- `queue-list-inform-driver-mockup.html` — Queue List with Inform Driver button + confirmation modal

### dock-group/ (feature paused — pending ops alignment)
- `yms-dock-group-animated.html` — animated demo
- `yms-dock-group-interactive.html` — interactive mockup

### driver-experience/
- `driver-experience-4234.html` — Driver experience 4.2.3.4 (EN)
- `driver-experience-4234-pt.html` — Driver experience 4.2.3.4 (PT)

---

## Pending Work

- **4.3.2.2** — Task-specific statuses (TBD) need alignment with LH/FM/LM teams
- **4.4 Queue List Visibility** — not started
- **6. Data Information** — data tables and logs for Gate Queue Control (gates events log, gate capacity status)
- **Dock Group feature** — paused, pending ops alignment on Option A vs B cargo compliance behavior
- **4.1.1.4 examples** — 100% compositions + absolute number rebuild (task #7, pending)

---

## Document Conventions
- Business requirements written in English
- Mockups are HTML files, self-contained, scale to window
- All mockups follow SPX Admin design system: Shopee orange #EE4D2D, dark sidebar #1a1f36
- Validation pattern: toggle freely activatable, fields always editable, validation only at Save
- Tables in BRs follow format: Context | Mockup / Illustration / Description
