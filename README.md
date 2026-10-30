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

## Run examples (Windows PowerShell)
```powershell
& "C:\Program Files\k6\k6.exe" run 01-first-test.js
& "C:\Program Files\k6\k6.exe" run --vus 5 --duration 20s 01-first-test.js
& "C:\Program Files\k6\k6.exe" run 04-pizza-api.js
& "C:\Program Files\k6\k6.exe" run a1-smoke.js

# Export an HTML report (example for average-load test)
$env:K6_WEB_DASHBOARD = "true"
$env:K6_WEB_DASHBOARD_PORT = "-1"
$env:K6_WEB_DASHBOARD_EXPORT = "reports/a2-average.html"
& "C:\Program Files\k6\k6.exe" run a2-average.js
Remove-Item Env:K6_WEB_DASHBOARD, Env:K6_WEB_DASHBOARD_PORT, Env:K6_WEB_DASHBOARD_EXPORT
```

## Public demo safety
QuickPizza is a shared public service. Never exceed 5 virtual users. Keep each run to 3 minutes or less except the required soak test, which uses only 2 virtual users for 10 minutes. Do not run breakpoint or hundreds-of-users tests against a site you do not own or have written permission to test.

See `RESULTS.md` for measurements recorded from actual runs.
