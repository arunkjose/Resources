---

# **Cron Job Cheatsheet (Linux Job Scheduling)**

## Basics
- Each user can manage their own **crontab**.
- Use `crontab -e` to edit your crontab (opens in the default editor).
- Format:  
  ```bash
  * * * * * command_to_execute
  ┬ ┬ ┬ ┬ ┬
  │ │ │ │ │
  │ │ │ │ └─ Day of the week (0 - 7) (Sunday=0 or 7)
  │ │ │ └─── Month (1 - 12)
  │ │ └───── Day of month (1 - 31)
  │ └─────── Hour (0 - 23)
  └─────────Minute (0 - 59)
  ```

---

## **Create a Cron Job (Every Minute)**
```bash
$ crontab -e
```
Add the line:
```bash
* * * * * echo "it is $(date)" >> /home/ubuntu/date-file
```

**Result Example:**
```
it is Thu Aug 31 03:43:01 UTC 2017
it is Thu Aug 31 03:44:01 UTC 2017
```

To verify:
```bash
$ cat /home/ubuntu/date-file
```
---
---

## **Remove All Cron Jobs of a User**
```bash
# crontab -r -u ubuntu
```

Check if cleared:
```bash
# crontab -l -u ubuntu
# Output: no crontab for ubuntu
```

---

## **Schedule Script on Specific Time & Days**
Run a command between **10:45 PM - 11:45 PM** on **Sun, Mon, Thu, Sat**:
```bash
# crontab -e 
```
Add:
```bash
1-45 22-23 * * 0,1,4,6 uptime >> /home/ubuntu/check-uptime
```

View result:
```bash
# cat /home/ubuntu/check-uptime
```

Sample Output:
```
 22:01:01 up 3 days,  5:21,  1 user,  load average: 0.00, 0.01, 0.05
 22:02:01 up 3 days,  5:22,  1 user,  load average: 0.00, 0.01, 0.05

```

---

## **Lab Task Summary**
### Task 1: Display Date Every Minute
```bash
# crontab -e
*/1 * * * * date >> date-file
```
Save and exit (`:wq` in `vi`)

View jobs:
```bash
# crontab -l
```

Check file:
```bash
# ls
# cat date-file
```
