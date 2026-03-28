---
name: Start TradingAgents App
description: Simple dependency check and run setup for TradingAgents CLI
type: project
---

# Start TradingAgents App Design

## Overview
Set up a proper development environment for the TradingAgents multi-agent trading framework and run the interactive CLI.

## Requirements
- User wants to use system Python (Python 3.14.3, pip 26.0)
- User has DEEPSEEK_API_KEY already configured in `.env` file
- Goal is to install dependencies and run `python -m cli.main`

## Approach: Simple dependency check and run
1. **Dependency verification**: Test if required packages are installed
2. **Installation**: Install missing dependencies via `pip install .`
3. **Validation**: Confirm `tradingagents` package imports successfully
4. **Execution**: Run `python3 -m cli.main` to start interactive CLI

## Steps

### 1. Check current installation status
- Test if `tradingagents` package imports without errors
- Identify missing dependencies from import tracebacks

### 2. Install dependencies
- Run `pip3 install .` to install package and all dependencies
- Verify installation completes without errors

### 3. Validate installation
- Test import of `TradingAgentsGraph` from main module
- Confirm no `ModuleNotFoundError` for core dependencies

### 4. Run the CLI
- Execute `python3 -m cli.main`
- Expect interactive interface for selecting:
  - Ticker symbols
  - Analysis date
  - LLM provider (DeepSeek based on `.env` configuration)
  - Research depth
  - Analyst teams to include

### 5. Expected outcome
- CLI presents welcome screen and configuration options
- User can proceed with trading analysis using DeepSeek API
- All agent teams (Research, Trading, Risk Management, Portfolio Management) execute

## Validation Criteria
- ✅ `pip3 install .` completes without errors
- ✅ `python3 -c "from tradingagents.graph.trading_graph import TradingAgentsGraph"` succeeds
- ✅ `python3 -m cli.main` launches interactive CLI interface
- ✅ CLI loads `.env` configuration including DEEPSEEK_API_KEY

## Notes
- Using system Python as requested (not virtual environment)
- Package installed in regular mode (not editable)
- DeepSeek API already configured in `.env` file
- Future updates require re-running `pip install .`