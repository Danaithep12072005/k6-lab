# How to review this lab

## Start here
1. Open `README.md` for setup and safe run commands.
2. Open `RESULTS.md` for actual measured results and the written Part B answers.
3. Open the test scripts in VS Code to inspect the code.
4. Open the HTML reports in a web browser to inspect time-series charts and thresholds.

## File map
- `01-first-test.js`: basic HTTP status check.
- `04-pizza-api.js`: POST to the pizza recommendation API and check the response.
- `05-no-token.js`: verify the API rejects an unauthenticated request with HTTP 401.
- `06-thresholds.js`: show a passing and deliberately failing p(95) threshold; `P95` is configurable via environment variable.
- `07-requirement.js`: translate a performance requirement into p(95), p(99), error-rate and check thresholds.
- `explore.js`: inspect topping ingredients and available tools.
- `08-bug-hunt.js`: reproduce and fix the case-sensitive ingredient/tool bug.
- `journey.js`: reusable user journey for home page, quotes, and pizza recommendation.
- `a1-smoke.js` to `a5-soak.js`: smoke, average-load, stress, spike and soak tests.
- `reports/a2-average.html`, `reports/a3-stress.html`, `reports/a4-spike.html`, `reports/a5-soak.html`: exported interactive HTML dashboards from the test runs.
- `RESULTS.md`: test metrics and reflections.
- `logs/`: local raw console output from the runs. Logs are excluded from Git to keep the submission focused.

## View reports
In File Explorer, open the `reports` folder and double-click an HTML report; it should open in the default browser. Use the report timeline and metric charts to compare latency and checks during the run.

## Run locally (PowerShell)
Run from the project folder:
```powershell
cd D:\Projects\k6-lab
& "C:\Program Files\k6\k6.exe" run a1-smoke.js
```

## Safety
The tests target the shared public QuickPizza demo. Do not exceed the lab's stated limit of 5 VUs; the soak test is limited to 2 VUs for 10 minutes. Do not use high-load tests against a public service without explicit authorization.
