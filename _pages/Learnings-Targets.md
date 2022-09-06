---
layout: page
title: Learning Targets
permalink: /learningtargets/
---

data = [["Tools Setup", "Create Fastpage, Creat first Jupyter notebook, Screen capture of VS Studio"], 
        ["Intro Python, Jupyter, Fastpages", "Productive Blogging, Jupyter Notebook using Bash, more], 
        ["Data Abstraction", "List/Dictionaries Iteration, HTML/Markdown Fragments"]
  
#define header names
col_names = ["Topic", "Notes/Reflections/Activities"]
  
#display table
print(tabulate(data, headers=col_names, tablefmt="fancy_grid", showindex="always"))