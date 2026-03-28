# DeepSeek API Integration Design

## Overview
Add DeepSeek API support to TradingAgents framework as an OpenAI-compatible provider.

## Requirements
- Support DeepSeek models: `deepseek-chat`, `deepseek-reasoner`, `deepseek-coder`
- Use `DEEPSEEK_API_KEY` environment variable
- API endpoint: `https://api.deepseek.com`
- Support optional `deepseek_thinking_level` configuration parameter

## Architecture
Treat DeepSeek as OpenAI-compatible provider using existing `OpenAIClient` class.

### Provider Flow
```
User Config → Factory → OpenAIClient → ChatOpenAI
  ↓                        ↓
"deepseek"          base_url="https://api.deepseek.com"
deep_think_llm      api_key=DEEPSEEK_API_KEY
quick_think_llm
```

## File Changes

### 1. `llm_clients/factory.py`
Add "deepseek" to provider check:
```python
if provider_lower in ("openai", "ollama", "openrouter", "deepseek"):
    return OpenAIClient(model, base_url, provider=provider_lower, **kwargs)
```

### 2. `llm_clients/openai_client.py`
Add to `_PROVIDER_CONFIG`:
```python
"deepseek": ("https://api.deepseek.com", "DEEPSEEK_API_KEY")
```

### 3. `llm_clients/validators.py`
Add DeepSeek models to `VALID_MODELS`:
```python
"deepseek": [
    "deepseek-chat",
    "deepseek-reasoner",
    "deepseek-coder",
]
```

### 4. `graph/trading_graph.py`
Add `deepseek_thinking_level` handling in `_get_provider_kwargs()`:
```python
elif provider == "deepseek":
    thinking_level = self.config.get("deepseek_thinking_level")
    if thinking_level:
        kwargs["thinking_level"] = thinking_level
```

## Configuration

### Environment Variables
Add to `.env.example`:
```bash
DEEPSEEK_API_KEY=
```

### Example Usage
```python
config = DEFAULT_CONFIG.copy()
config["llm_provider"] = "deepseek"
config["deep_think_llm"] = "deepseek-reasoner"
config["quick_think_llm"] = "deepseek-chat"
config["deepseek_thinking_level"] = "high"  # Optional
```

## Testing Strategy
1. Environment setup: Verify `DEEPSEEK_API_KEY` loading
2. Factory test: Confirm "deepseek" creates `OpenAIClient`
3. Model validation: Test DeepSeek models accepted
4. Configuration test: Verify `deepseek_thinking_level` parameter
5. Integration test: Run existing `main.py` with DeepSeek config

## Edge Cases
- Missing API key: Graceful failure with clear error
- Invalid model: `validate_model()` returns `False`
- Network issues: Existing retry/timeout logic applies
- Base URL override: Users can set custom `backend_url`

## Dependencies
- No new dependencies required (uses existing `langchain_openai`)
- Compatible with current LangChain OpenAI client

## Success Criteria
- DeepSeek provider recognized in factory
- Models validated correctly
- API calls use correct endpoint and authentication
- Optional `deepseek_thinking_level` parameter supported