# AI-research-project
# 🧠 AI Self-Debugger: Complete Execution Coverage Using LLMs

![License](https://img.shields.io/badge/license-MIT-blue.svg)  
**Author:** Mukesh Shaganti  
**Affiliation:** Mukesh Shaganti Research  
**Contact:** mukeshshaganti@gmail.com  

---

## 📌 Overview

This project introduces a proof-of-concept AI system that uses LLMs to:

- 🔁 Automatically run every possible function or execution path
- 🐞 Detect and interpret runtime errors
- 🔧 Suggest and apply intelligent fixes

Inspired by modern compiler design, software testing, and LLM-based reasoning, this framework aims to **simulate the behavior of an autonomous AI engineer**.

---

## 🏗️ How It Works

1. ✅ Parse Python functions using `ast`  
2. ⚙️ Dynamically call each function  
3. 🚨 Catch errors during execution  
4. 💡 Suggest fixes (via LLM simulation or GPT API in real integration)

---

## 🧪 Example

```python
def divide(a, b):
    return a / b

def buggy_function():
    return unknown_variable + 1
