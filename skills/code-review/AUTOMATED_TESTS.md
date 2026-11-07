# Automated tests: review criteria

A good test fails when the behaviour it covers breaks, and passes when it doesn't.

## Good tests
- Test behaviour, not implementation: assert on return values and observable side effects through the public interface.
- Expected values come from outside the code under test: hardcoded literals, known examples, or worked-out cases.
- One behaviour per test. The name states scenario and outcome, e.g. `returns 404 when user does not exist`.
- Cover edge cases and failure paths, not just the happy path: empty input, boundaries, invalid data, errors.
- Deterministic: no dependence on real time, randomness, network, or test order.
- Mock only at system boundaries (network, filesystem, clock, third-party services).

## Bad tests (flag in review)
- **Tautological**: the expected value is produced by the same logic as the code under test, so the test cannot fail.
  - `expect(calcTax(100)).toBe(100 * TAX_RATE)` → bad, repeats the formula
  - `expect(calcTax(100)).toBe(24)` → good, independent value
  - Asserting a mock returns what it was configured to return is also tautological.
- **Implementation-coupled**: asserts on private methods, internal call order, or call counts when only the outcome matters. Breaks on harmless refactors.
- **Over-mocked**: so much is mocked that the test only exercises the mocks.
- **Weak assertions**: only checks that code runs without throwing, or uses `toBeDefined()` when a specific value is known.
- **Blind snapshots**: large snapshots that get re-recorded without review.
- **Flaky**: depends on timing, sleeps, shared state, or live external services.
- **Testing the framework**: e.g. a setter followed by a getter, or that the ORM saves a record.

## Check every test with three questions
1. If the implementation were broken, would this test fail?
2. Where does the expected value come from? If from the code under test (or a copy of its logic), it's tautological.
3. Would a refactor that keeps behaviour the same break this test? If yes, it's coupled to implementation.