---
title: "Automating My Life with Python"
date: 2026-01-30
draft: false
description: "How I use Python scripts to handle emails, track expenses, and organize files."
summary: "Real-world examples of automation scripts I run daily. Includes code snippets and Asciinema demo."
tags: ["Python", "Automation", "Scripting", "Productivity"]
series: ["Python Deep Dive"]
featuredImage: "https://images.unsplash.com/photo-1518770660439-4636190af475?q=80&w=2070&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
Why spend 10 minutes doing it every day when you can spend 10 hours automating it once? (Just kidding. It pays off eventually.)
{{< /lead >}}

## 1. The File Organizer

I download a lot of files. My `Downloads` folder is a mess. I wrote a script to watch the folder and move files based on extension.

```python
import os
import shutil

EXTENSIONS = {
    "Images": [".jpg", ".png", ".svg"],
    "Documents": [".pdf", ".docx", ".txt"],
    "Installers": [".deb", ".iso", ".zip"]
}

def organize():
    for filename in os.listdir("."):
        for folder, exts in EXTENSIONS.items():
            if filename.endswith(tuple(exts)):
                shutil.move(filename, folder)
```

## 2. Terminal Demo

Here is the script in action:

{{< asciinema id="113337" >}}
*(Note: This is a demo recording)*

## 3. Expense Tracking

I use `pandas` to parse my bank's CSV export and categorize expenses automatically.

```python
import pandas as pd

df = pd.read_csv("statement.csv")
food = df[df['description'].str.contains("UBER EATS|CAFE")]
print(f"Total Food: ${food['amount'].sum()}")
```

{{< alert icon="robot" >}}
**Tip**: Run these scripts on a cron job or systemd timer so you never have to think about them.
{{< /alert >}}
