# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a k6 load testing project template for performance testing. The project is structured around Grafana k6 for conducting different types of performance tests.

## Commands

### Testing Commands
- `npm run test:smoke` - Run smoke tests (basic functionality verification with 1 VU for 1 minute)
- `npm run test:load` - Run load tests (gradual ramp-up to 400 concurrent users over 39 minutes)
- `npm run test:stress` - Run stress tests (extended load testing up to 600 concurrent users over 42 minutes)

### Direct k6 Commands
- `k6 run tests/smoke/smoke-test.js` - Execute smoke test directly
- `k6 run tests/load/basic-load-test.js` - Execute load test directly
- `k6 run tests/stress/stress-test.js` - Execute stress test directly

## Test Architecture

### Test Categories
The project organizes tests into three distinct categories based on testing objectives:

- **Smoke Tests** (`tests/smoke/`): Minimal load tests to verify basic functionality and system availability
- **Load Tests** (`tests/load/`): Sustained load tests that gradually increase user load to test normal expected traffic
- **Stress Tests** (`tests/stress/`): High-load tests that push the system beyond normal capacity to identify breaking points

### Test Configuration Patterns
- Smoke tests use simple VU/duration configuration for quick validation
- Load and stress tests use staged ramping patterns for realistic traffic simulation
- All tests include basic HTTP status and response time validations
- Default target URL is `https://test.k6.io` (should be changed to actual test targets)

### Key Testing Principles
- Tests follow k6 ES6 module patterns with import statements
- Each test includes response validation using k6's `check()` function
- Sleep intervals (1 second) simulate realistic user behavior between requests
- Staged load patterns allow for gradual system warm-up and cool-down periods