---

# **Lab: Getting Started with Jira Service Management for IT Support**

---

## **Part 1: Create a Free Jira Account (5–10 mins)**

1. Go to: [https://www.atlassian.com/software/jira/service-management](https://www.atlassian.com/software/jira/service-management)
2. Click **“Get it free”**
3. Sign up with **Google or Email**
4. Choose:
   - Product: **Jira Service Management**
   - Site name: e.g., `yourteamname.atlassian.net`
   - Team type: **IT team**
5. Once loaded, you’re in your **Jira dashboard**.

---

## **Part 2: Create Your First Service Project (10 mins)**

1. Click **Projects** → **Create Project**
2. Choose **IT Service Management** template → Click **Use Template**
3. Name it: `IT Helpdesk` → Click **Create Project**
4. Your service desk is now ready!

---

## **Part 3: Create Sample Tickets (15 mins)**

### Create 3 Sample Tickets:

| Type            | Summary                          | Description                           | Priority |
|------------------|----------------------------------|---------------------------------------|----------|
| Incident         | “Email not working”              | “User unable to send mail via Outlook”| P1       |
| Service Request  | “Need access to Jenkins”         | “New joiner needs Jenkins permissions”| P3       |
| Problem          | “Frequent VPN drops”             | “Reported by 4 users every morning”   | P2       |

### Actions:
- Click **Create** → Choose correct type
- Assign to yourself
- Add a **comment** and **status** like “In Progress”, “Resolved”

---

## **Part 4: Apply SLA Rules (15–20 mins)**

1. Go to `Project settings` → **SLAs**
2. Click **Add SLA**

### SLA 1 – First Response:
- Name: **First Response Time**
- Time goal: **15 minutes** (for P1)
- Start counting: **Issue created**
- Stop counting: **First response**
- Calendar: **24/7**
- Condition: `Priority = P1`

### SLA 2 – Time to Resolution:
- Name: **Resolution SLA**
- Time goal:
  - P1: 4 hours
  - P2: 8 hours
  - P3: 24 hours
- Condition: Set based on priority

3. Save and test with your sample tickets.

---

## **Optional: Create Automation Rule for Auto-Closure (10 mins)**

1. Go to: **Project Settings → Automation**
2. Click **Create Rule**
3. Choose:
   - Trigger: Issue transitioned to “Resolved”
   - Condition: Status = Resolved for 2 days
   - Action: Transition to “Closed”
4. Save and test

---

## **Lab Summary & Deliverables:**
- ✅ Jira account created
- ✅ IT service project set up
- ✅ 3 ticket types created and worked
- ✅ SLAs configured (first response + resolution)
- ✅ Optional automation setup

---

