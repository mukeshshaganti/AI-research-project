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
🧪 Example

import ast
import inspect
import traceback

class AISelfDebugger:
    def __init__(self, code: str):
        self.code = code
        self.parsed = ast.parse(code)
        self.function_names = [n.name for n in self.parsed.body if isinstance(n, ast.FunctionDef)]

    def execute_all(self):
        print("🔍 Starting autonomous function analysis...\n")
        try:
            exec(self.code, globals())
        except Exception as e:
            print("❌ Failed to load code:", str(e))
            return

        for fn_name in self.function_names:
            print(f"=== Function: {fn_name} ===")
            try:
                args = self.get_dummy_args(fn_name)
                result = eval(f"{fn_name}(*{args})")
                print(f"✅ Output: {result}")
            except Exception as e:
                print(f"❌ Error: {type(e).__name__}: {e}")
                self.suggest_fix(e)
            print()

    def get_dummy_args(self, fn_name):
        try:
            fn = eval(fn_name)
            sig = inspect.signature(fn)
            args = []
            for param in sig.parameters.values():
                if param.annotation == int or param.name in ['a', 'b', 'x', 'y']:
                    args.append(1)
                elif param.annotation == str or param.name in ['name']:
                    args.append("'Test'")
                else:
                    args.append(1)
            return tuple(args)
        except Exception:
            return tuple()

    def suggest_fix(self, error):
        msg = str(error)
        if "division by zero" in msg:
            print("💡 Suggestion: Add a zero-check before performing division.")
        elif "is not defined" in msg:
            print("💡 Suggestion: Ensure all variables are defined before use.")
        elif "unsupported operand type" in msg:
            print("💡 Suggestion: Check for type mismatches in operations.")
        else:
            print("💡 Suggestion: Use a debugger or GPT to analyze this error.")

# Sample user code to test
user_code = \"\"\"
def divide(a, b):
    return a / b

def greet(name):
    print("Hello, " + name)

def buggy_function():
    return unknown_variable + 1

def multiply(x, y):
    return x * y
\"\"\"

if __name__ == "__main__":
    debugger = AISelfDebugger(user_code)
    debugger.execute_all()
