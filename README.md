# Logger

Hi and welcome to the **Logger** 👋

The logger is an automated data collection tool to help you during the UX testing sessions. It is created as a **plug-in**, so there is no need to modify your source code, you only need to inject the logger script into your prototype (HTML prototypes).

It is part of a Master's Thesis at FIIT STU 👩‍🎓

If you have any questions, don't hesitate to contact me via:
- **Teams**: Darina Dvorecká
- **Discord**: dada25

If you use this logger, please send me your exported ``.json`` files for my further research ✨

**Thank you for the contribution 🫶**

---

## 🛠️ How to Install

Include the `logger.js` script in your prototype HTML file (if you have multiple HTML files you need to include this script in each file)

```html
<script src="logger.js"></script>
```

Then you just normally open your HTML file in a browser and the logger panel will automatically appear in the bottom-right corner.

---

## 📁 Task Configuration

The logger is designed to be **task-based** and automatically switch between tasks. So before you start with your UX testing session, you need to prepare and create a task configuration file in ``.json`` format.

Here is an example of a configuration file:

```json
[
  {
    "description": "Find the contact information of the author",
    "type": "find",
    "question": "What is the author's email address?",
    "maxTime": 60
  },
  {
    "description": "Navigate to the loan request page",
    "type": "do",
    "endElement": "#loanPageButton",
    "maxTime": 45
  }
]
```

To configure your tasks, upload your ``.json`` file using the **Load Tasks** button in the logger panel.

---

## 📝 Supported Task Types

This version of the logger supports two main types of tasks:
- **find** - the task is based on locating specific information, there is no end element to be clicked on
- **do** - the task is based on interacting with an end element to complete the task (e.g. create an order and finish your order)

If you need specific type of task e.g. for the **Wizard of Oz** during annotation creation, just contact me.

### 🔍 find 

Use this type when the participant must **locate** some kind of **information**.

**Required fields**:

| Field | Description |
|-------|-------------|
| description | Task description |
| type | `"find"` |
| question | Question to verify task success |
| maxTime | Time limit in seconds |

After completing the task, the participant will:

- input the answer
- rate task difficulty (1–7)

### 🧑‍💻 do

Use this type for **interaction-based** tasks.

Required fields:

| Field | Description |
|-------|-------------|
| description | Task description |
| type | `"do"` |
| endElement | CSS selector indicating task completion |
| maxTime | Time limit in seconds |

Task completion is automatically triggered when the participant clicks an element matching the given CSS selector. The *task difficulty rating* modal appears 2 seconds after clicking the end element.

Example of ``endElement``:

- ``#id`` — element ID e.g. ``"#add-to-cart"``
- ``.class`` — CSS class e.g. ``".dropdown-toggle"``
- ``tagname`` — element type (button, a, etc.)
- CSS selector ``"button[type='submit']"``

--- 

## ⏱️ Timeout Handling

Each task has a defined time limit (`maxTime`).

If exceeded:

- the task continues running
- it is marked as **not completed in time**
- completion can still occur afterward

---

## 📤 Export

After completing all tasks, click **Export** to download:

```
task_log_TIMESTAMP.json
```

---

## 💾 Persistence

Logger state is stored in ``localStorage``

This allows:
- session recovery after refresh
- persistence across page transitions
- uninterrupted task tracking

State is automatically cleared after exporting results.

---

## ⚠️ Notes

- Logging only occurs when a task is active
- Logging pauses during modals
- Invalid task files will be rejected
- Tasks can be skipped before starting