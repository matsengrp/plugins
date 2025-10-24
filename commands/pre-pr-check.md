---
description: Run comprehensive pre-PR quality checklist
---

# Pre-PR Quality Checklist

You are helping the user prepare code for a pull request by guiding them through a comprehensive quality checklist. This is based on rigorous clean code principles and testing standards.

## Your Role

Guide the user through each step of the checklist systematically. For each step:
1. Explain what needs to be done
2. Execute the required checks/commands
3. Report the results clearly
4. Only proceed to the next step after current step passes or user acknowledges issues

## Checklist Steps

### 1. Issue Compliance Verification (CRITICAL - Do This First!)
- Ask the user for the GitHub issue number they're working on
- Use `gh issue view <number>` to fetch the issue details
- Review ALL requirements in the issue
- Verify 100% completion of specified requirements
- If any requirement cannot be met, STOP and discuss with user before proceeding

### 2. Code Quality Foundation

**Format Code:**
- Run `make format` to apply ruff formatting and fixes
- Report any files that were modified

**Documentation Check:**
- Scan modified files for functions without docstrings
- Flag any non-trivial functions missing comprehensive docstrings
- Remind about Google-style docstring format with Args/Returns sections

### 3. Architecture and Implementation Review

**Antipattern Scan:**
- Use the Task tool with subagent_type="antipattern-scanner" on all new/modified code
- Look for: SRP violations, dependency inversion failures, naming issues
- Report findings and wait for user to address before continuing

**Clean Code Review:**
- Use the Task tool with subagent_type="clean-code-reviewer" on all new/modified code
- Check: single responsibility, meaningful names, small functions, DRY violations
- Report findings and wait for user to address before continuing

**Design Compliance:**
- Ask user to confirm implementation matches intended design
- If design document exists, cross-reference it

### 4. Test Quality Validation

**Test Implementation Audit (CRITICAL):**
- Scan ALL test files for:
  - Partially implemented tests (just `pass` statements)
  - Placeholder implementations
  - Mock objects that return fake data
  - Identity functions or trivial arithmetic in tests
- **Anti-Fake Test Barrier**: Flag any tests that use fake implementations
- Remind: All tests must validate REAL behavior with REAL data
- Use fixtures from `tests/conftest.py` for real data

**Integration Tests:**
- Run `make test` to execute all tests
- Report pass/fail status
- If failures exist, STOP and require fixes before proceeding

**Test Coverage:**
- Run `pytest --cov=loris tests/` (adjust package name as needed)
- Report coverage percentage
- Flag any critical code paths with low coverage

### 5. Final Static Analysis

**Quality Checks:**
- Run `make check` to verify all static analysis (ruff, mypy, TODOs)
- Report any violations
- Require fixes before proceeding

**Format Check:**
- Run `make checkformat` to verify ruff formatting compliance
- If this fails after step 2, investigate what changed

## Success Criteria

All steps must pass before PR creation:
- ✅ All issue requirements completed
- ✅ Code formatted (make format)
- ✅ All functions documented
- ✅ No antipatterns detected (or acknowledged/fixed)
- ✅ Clean code review passed (or issues addressed)
- ✅ No fake/partial tests detected
- ✅ All tests passing (make test)
- ✅ Adequate test coverage
- ✅ All static analysis passing (make check)
- ✅ Format verification passing (make checkformat)

## Final Output

After completing all steps, provide:
1. Summary of checklist completion status
2. List of any remaining concerns or warnings
3. Confirmation that code is ready for PR, OR list of items that need attention
4. Reminder about fail-fast principles and real testing standards

## Important Notes

- **Fail Fast**: Stop at first major issue - don't continue if critical problems exist
- **No Fake Tests**: Zero tolerance for mock implementations that return fake data
- **Real Validation**: Every test must validate actual system behavior
- **Issue Compliance**: 100% requirement completion is mandatory

If the project doesn't have a Makefile with these commands, adapt the commands to what's available in the project (e.g., direct pytest, ruff, mypy commands).
