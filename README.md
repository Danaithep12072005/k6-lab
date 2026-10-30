# Grafana k6 Performance Testing Lab

Repository for the ITDS362 Software Quality Assurance and Testing lab, "Performance Testing with Grafana k6".

## Contents
- Part 0: basic HTTP tests, API checks, thresholds, requirement test, and bug hunt.
- Part A: shared user journey, smoke, average-load, stress, spike, and soak tests.
- `reports/`: HTML reports exported from the actual test runs.
- `RESULTS.md`: observed metrics and reflections.

## Requirements
- Windows, macOS, or Linux
- Grafana k6 installed: https://grafana.com/docs/k6/latest/set-up/install-k6/
- Internet connection to the shared QuickPizza demo at https://quickpizza.grafana.com/

## Run examples
```powershell
k6 run 01-first-test.js
k6 run --vus 5 --duration 20s 01-first-test.js
k6 run 04-pizza-api.js
k6 run a1-smoke.js
k6 run --out web-dashboard=export=reports/a2-average.html a2-average.js
```

## Public demo safety
QuickPizza is a shared public service. Never exceed 5 virtual users. Keep each run at 3 minutes or less except the required soak test, which uses only 2 virtual users for 10 minutes. Do not run breakpoint or hundreds-of-users tests against a site you do not own or have written permission to test.

See `RESULTS.md` for measurements recorded from actual runs.
