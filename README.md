# CST8917_Lab03

#  Teams Chat Moderation Logic App – CST8917 Lab 3

##  Objective

This project implements a Microsoft Teams **chat moderation system** using **Azure Logic Apps**. It automatically detects inappropriate messages in real-time and alerts an administrator via **email**.

---

##  Technologies Used

- Azure Logic Apps
- Microsoft Teams Connector
- Outlook 365 Connector (Email)
- HTML-based notification content
- Optional: Azure Cognitive Services

---

##  Workflow Steps

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/247cc19f-7496-472e-b616-0ba91772854f" />


1. **Trigger:** Logic App listens for a new message in a Teams channel
2. **Condition:** Evaluates if the message contains any inappropriate words (e.g., "bad", "hate", "stupid")
3. **If TRUE:** Sends an email notification to the admin
4. **If FALSE:** Does nothing

---

##  Moderation Logic (Expression Used)

```plaintext
or(
  contains(triggerBody()?['body'], 'bad'),
  contains(triggerBody()?['body'], 'hate'),
  contains(triggerBody()?['body'], 'stupid')
)
```

---

##  Email Alert Format

```html
<p><strong>Policy Violation Detected</strong></p>

<p><strong>User:</strong> @{
  body('from.user.displayName')
}</p>
<p><strong>Message:</strong> @{
  body('body.content')
}</p>
<p><strong>Violation Reason:</strong> Inappropriate content detected via moderation.</p>

<p>🔍 Please review the conversation in Microsoft Teams and take appropriate action.</p>
```

---

##  Test Cases

| Message                        | Triggered? | Result     |
|-------------------------------|------------|------------|
| “Good job team!”              | ❌         | No email   |
| “stupid”                      | ✅         | Email sent |


---

##  How to Run/Test

1. Open Microsoft Teams and post a message to your selected channel
2. If the message contains a flagged word, check the admin email
3. Go to Azure Portal > Logic App > Run History to view execution logs

---

##  Lessons Learned

- Logic Apps simplifies workflow automation without needing code
- Expression editor supports inline content policy logic
- Real-time moderation can be easily extended with AI

---

##  Demo Video
https://youtu.be/rheQoDF6w0c
