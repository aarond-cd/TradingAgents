# Start TradingAgents App Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Install TradingAgents dependencies and run the interactive CLI using system Python.

**Architecture:** Simple dependency check and installation using pip, then execute the CLI module directly. Uses existing .env configuration with DEEPSEEK_API_KEY.

**Tech Stack:** Python 3.14.3, pip 26.0, TradingAgents package dependencies (langgraph, langchain, yfinance, etc.)

---

### Task 1: Check current installation status

**Files:**
- Test: N/A (command-line verification)

- [ ] **Step 1: Test tradingagents package import**

```bash
python3 -c "import tradingagents" 2>&1
```

Expected: No output if successful, error if not installed

- [ ] **Step 2: Check for missing dependencies**

```bash
python3 -c "from tradingagents.graph.trading_graph import TradingAgentsGraph" 2>&1
```

Expected: Either success or ModuleNotFoundError showing missing packages

- [ ] **Step 3: Commit initial status**

```bash
git add docs/superpowers/plans/2026-03-27-start-tradingagents-app.md
git commit -m "chore: add implementation plan for starting TradingAgents app"
```

---

### Task 2: Install dependencies

**Files:**
- Modify: System Python packages via pip

- [ ] **Step 1: Install TradingAgents package and dependencies**

```bash
pip3 install .
```

Expected: Installation completes with "Successfully installed tradingagents-0.2.2" and all dependencies

- [ ] **Step 2: Verify installation output**

```bash
pip3 list | grep tradingagents
```

Expected: Shows `tradingagents 0.2.2`

- [ ] **Step 3: Commit after installation**

```bash
git commit -m "chore: install TradingAgents dependencies" --allow-empty
```

---

### Task 3: Validate installation

**Files:**
- Test: N/A (import verification)

- [ ] **Step 1: Test main module import**

```bash
python3 -c "from tradingagents.graph.trading_graph import TradingAgentsGraph; print('TradingAgentsGraph import successful')"
```

Expected: Prints "TradingAgentsGraph import successful" with no errors

- [ ] **Step 2: Test CLI module import**

```bash
python3 -c "from cli.main import app; print('CLI app import successful')"
```

Expected: Prints "CLI app import successful" with no errors

- [ ] **Step 3: Verify .env file exists**

```bash
grep -n "DEEPSEEK_API_KEY" .env
```

Expected: Shows line with DEEPSEEK_API_KEY value

- [ ] **Step 4: Commit validation results**

```bash
git commit -m "test: verify TradingAgents installation" --allow-empty
```

---

### Task 4: Run the CLI

**Files:**
- Execute: CLI module

- [ ] **Step 1: Start interactive CLI**

```bash
python3 -m cli.main
```

Expected: CLI launches with welcome screen and interactive prompts

- [ ] **Step 2: Test basic CLI functionality**

Press Ctrl+C to exit after confirming CLI loads

- [ ] **Step 3: Commit successful execution**

```bash
git commit -m "feat: successfully run TradingAgents CLI" --allow-empty
```