# Coding Standards

Standards for writing code across all projects. Used by specialized agents (rails-expert, etc.) and main Claude Code sessions.

## Core Principle: Clarity Through Structure

Self-documenting code over comments. Refactor with better names instead of adding explanatory comments.

**Never add comments** unless explicitly requested by the user.

When refactoring instead of commenting:
1. Rename variables/methods to make intent obvious
2. Extract well-named functions
3. Restructure code to be self-explanatory

**Example - Bad:**
```ruby
# Calculate the total price with tax
def calc_total(price, tax_rate)
  # Multiply price by tax rate
  result = price * (1 + tax_rate)
  return result  # Return the result
end
```

**Example - Good:**
```ruby
def calculate_total_with_tax(price, tax_rate)
  price * (1 + tax_rate)
end
```

## Project Organization

Save work artifacts in `.claude/<branch-name>/` (excluded from git via .gitignore)
