# ARG25 Project Submission

Invisible Garden -- ARG25.

This is not my first project, but I am excited to do some protocol work and might submit this as my main one.


##  Project Title
Minimal Implementation of Spec Test Sequence Trace Framework (based on Issue #4603)

// Spec test sequence trace, a general test vector format for the Ethereum consensus layer

// https://github.com/ethereum/consensus-specs/issues/4603

## Team
- Team/Individual Name: Ivan Anishchuk
- GitHub Handles: IvanAnishchuk
- Devfolio Handles: ivananishchuk

## Project Description

What are you building and why does it matter?

We are implementing a minimal, functional version of the "spec test sequence trace" framework proposed in ethereum/consensus-specs#4603

// XXX AI slop ahead, please fix before submission

**The Problem:**

The current consensus-spec test format (in .yaml) is excellent for "one-shot" tests (given input, check output). However, it's not well-suited for "sequence tests" that model a series of state changes over time, such as complex fork-choice scenarios, state-transition chains, or sync processes. Writing these tests currently requires a lot of Python boilerplate, mixing test setup with test logic, making them hard to read, maintain, and reuse.

**Our Solution:**

This project will build a minimal Python-based test runner (a "harness") that parses a new, simple YAML "trace" format. This format defines a sequence of operations (e.g., `init_state`, `tick`, `process_block`, `assert_head`).

This approach separates the test logic (the declarative YAML trace) from the test execution (the Python harness), making sequence tests far cleaner, more powerful, and easier for all client teams to use.

We are going to use wrapt-based decorator, no?



## Tech Stack
_List all the technologies, frameworks, and tools you are using._

Core: Python 3 (3.13 is the latest supported by the spec project)

Important libraries: pyyaml, wrapt

Testing: pytest

Ethereum Knowledge: Deep understanding of the Beacon Chain state transition function, fork choice, and the pyspecs test architecture.

Tooling: Git, GitHub

The Spec: https://github.com/ethereum/consensus-specs


## Objectives
_What are the specific outcomes you aim to achieve by the end of ARG25?_

1. Define Minimal Spec: Define a minimal .yaml spec for the test trace, supporting at least 3-4 key operations (e.g., `init_state`, `tick`, `process_block`, `assert_head`).

2. Build Trace Runner: Implement a Python pytest helper/fixture that can parse and execute a test trace file step-by-step.

3. Implement Handlers: Write the Python "handler" functions for the minimal operations defined in Objective 1.

4. Convert One Test: Identify one existing complex, stateful test from the pyspecs suite and convert it to the new trace format.

5. Pass Test: Successfully run the new trace test and have it pass, proving the framework is functional.

6. Submit PR: Have a clean, well-documented Pull Request (even if in "Draft" state) ready for submission to ethereum/consensus-specs to demonstrate the proof-of-concept.


## Weekly Progress

### Week 1 (ends Oct 31)
**Goals:**

- Research: Deep dive into Issue #4603 and, more importantly, the existing pyspecs test harness. Understand how tests are currently discovered and run by pytest.

- Identify: Select 1-2 existing tests (e.g., a simple fork-choice test) that are good candidates for conversion.

- Define: Finalize the minimal YAML spec for the trace. Define the exact structure for operations like `init_state`, `tick`, `process_block`, and `assert_state`.

- Plan: Design the core architecture of the Python test runner. How will it be invoked by pytest? Not sure it's going to be a runner, probably a decorator-based approach using wrapt is enough.

**Progress Summary:**

Started research.

### Week 2 (ends Nov 7)
**Goals:**

- Build Runner: Write the core Python script that parses the new YAML trace files.
- Implement Handlers (Core): Implement the Python functions for `init_state` (or loading genesis) and tick.
- Implement `process_block`: Implement the handler for submitting a block to the state.
- Initial Conversion: Convert the chosen test case into the new .yaml trace format.
- Debug: Get the runner to successfully parse and attempt to execute the full trace, even if assertions fail.

**Progress Summary:**


### 🗓️ Week 3 (ends Nov 14)
**Goals:**

- Implement Assertions: Implement the assert_... handler (e.g., `assert_head`, `assert_state_root`) to make the test actually check for correctness.
- Pass Test: Debug the handlers and runner until the converted test case passes successfully.
- Refactor & Document: Clean up the runner code, add comments, and write a brief explanation in the PR of how to use the new framework.
- Final PR: Prepare and submit the final Pull Request for review, clearly showing the "before" (old test) and "after" (new trace) to demonstrate the value.

**Progress Summary:**



## Final Wrap-Up
_After Week 3, summarize your final state: deliverables, repo links, and outcomes._

- **Main Repository Link:**  (Link to your fork of ethereum/consensus-specs)
- **Demo / Deployment Link (if any):**  (Link to the PR submitted to ethereum/consensus-specs)
- **Slides / Presentation (if any):** (make them)



## 🧾 Learnings
_What did you learn or improve during ARG25?_



## Next Steps
_If you plan to continue development beyond ARG25, what’s next?_



_This template is part of the [ARG25 Projects Repository](https://github.com/invisible-garden/arg25-projects)._
_Update this file weekly by committing and pushing to your fork, then raising a PR at the end of each week._
