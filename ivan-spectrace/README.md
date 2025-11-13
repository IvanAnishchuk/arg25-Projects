# ARG25 Project Submission

Invisible Garden -- ARG25.

##  Project Title
Minimal Implementation of Spec Test Sequence Trace Framework (based on Issue #4603)

## Team
- Team/Individual Name: Ivan Anishchuk
- GitHub Handles: IvanAnishchuk
- Devfolio Handles: ivananishchuk

## Project Description

What are you building and why does it matter?

I am implementing a minimal, functional prototype of the "spec test sequence trace" framework proposed in ethereum/consensus-specs#4603

**The Problem:**

The current consensus-spec test suite is good but we want to write tests in a more linear way and generate test vectors from everything. First step is to implement a proxy wrapper for the spec object passed to tests in way that it can trace method calls and save them in a nice YAML format with states and other heavy objects being hashed and stored in SSZ files. That will provide infrastructure for "sequence tests" that model a series of state changes over time, such as complex fork-choice scenarios, state-transition chains, or sync processes. Writing these tests currently requires a lot of Python boilerplate, mixing test setup with test logic, making them hard to read, maintain, and reuse. There will be many other improvements along the way and it's not quite final version ready for submission to the main repo, but this is a first step towards that goal and demostrates my knowledge of the protocol and consensus spec repo.

**Our Solution:**

This project adds a minimal wrapt-based wrapper proxy and a decorator for the spec to save traces in a simple YAML "trace" format. This format defines a sequence of operations (e.g., `init_state`, `tick`, `process_block`, `assert_head`).

This approach separates the test logic (the declarative YAML trace) from the test execution (the Python harness), making sequence tests far cleaner, more powerful, and easier for all client teams to use.




## Tech Stack
_List all the technologies, frameworks, and tools you are using._

Core: Python 3 (3.13 is the latest supported by the spec project)

Important libraries: pyyaml, wrapt, pydantic

Testing: pytest

Ethereum Knowledge: Deep understanding of the Beacon Chain state transition function, fork choice, and the pyspecs test architecture.

Tooling: Git, GitHub

The Spec: https://github.com/ethereum/consensus-specs

My PR draft: https://github.com/IvanAnishchuk/eth-consensus-specs/pull/1


## Objectives
_What are the specific outcomes you aim to achieve by the end of ARG25?_

1. Define Minimal Requirements: Define a minimal .yaml spec for the test trace, supporting at least 3-4 key operations (e.g., `init_state`, `tick`, `process_block`, `assert_head`).

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

Researched and clarified the goals, implemented the initial prototype.

### 🗓️ Week 3 (ends Nov 14)
**Goals:**

- Implement Assertions: Implement the assert_... handler (e.g., `assert_head`, `assert_state_root`) to make the test actually check for correctness.
- Pass Test: Debug the handlers and runner until the converted test case passes successfully.
- Refactor & Document: Clean up the runner code, add comments, and write a brief explanation in the PR of how to use the new framework.
- Final PR: Prepare and submit the final Pull Request for review, clearly showing the "before" (old test) and "after" (new trace) to demonstrate the value.

**Progress Summary:**

Cleaned up the prototype, its unit tests and converted example test cases and prepared for final submission.


## Final Wrap-Up
_After Week 3, summarize your final state: deliverables, repo links, and outcomes._

- **Main Repository Link:** https://github.com/IvanAnishchuk/eth-consensus-specs/
- **Demo / Deployment Link (if any):**  https://github.com/IvanAnishchuk/eth-consensus-specs/pull/1/files
- **Slides / Presentation (if any):** n/a



## 🧾 Learnings
_What did you learn or improve during ARG25?_

A lot about the protocol, the consensus-specs repo, and how to write better tests for it. Also improved my Python skills, especially with dynamic proxies and decorators using wrapt.

## Next Steps
_If you plan to continue development beyond ARG25, what’s next?_

I plan to continue refining the framework, adding more operations and improving usability. Eventually, I hope to get the PR merged into the main consensus-specs repo and advocate for its adoption by other client teams. If it turns out to be a good match I would like to continue contributing to the consensus-specs repo in future, even in full-time capacity.

