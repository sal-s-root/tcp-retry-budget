# tcp-retry-budget

Estimate the maximum configured connection-attempt time including exponential retry delays.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "attempts": 3,
  "timeout_seconds": 2,
  "backoff_seconds": 1
}
```

Result:

```json
{
  "attempts": 3,
  "backoff_delays_seconds": [
    1.0,
    2.0
  ],
  "configured_budget_seconds": 9.0
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

A model rather than a network probe; excludes DNS, scheduling, jitter, and application processing.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [subnet-capacity-calculator](https://github.com/sal-s-root/subnet-capacity-calculator), [http-access-log-summary](https://github.com/sal-s-root/http-access-log-summary).
