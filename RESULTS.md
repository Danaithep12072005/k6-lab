# K6 lab results

> Measurements in this file must come from the actual runs on this computer. Fill-in fields are intentionally left blank until each run finishes; do not treat sample numbers from the handout as this machine's results.

## Part 0
- Step 0.1, http_req_duration:
- Step 0.2, requests, rate and p(95), and why the rate stays below 5:
- Step 0.6, exit code of the normal run and of the run with P95=300:
- Step 0.7, rules that passed, p(95), p(99), exit code after your change:
- Step 0.8, what was wrong, and how the checks showed it:

## Part A results
| Step | Test type | Users | Req/s | p(95) | Max | Failed | Checks |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: |
| A1 | Smoke | 1 | TBD | TBD | TBD | TBD | TBD |
| A2 | Average load | 3 | TBD | TBD | TBD | TBD | TBD |
| A3 | Stress | 5 | TBD | TBD | TBD | TBD | TBD |
| A4 | Spike | 5 | TBD | TBD | TBD | TBD | TBD |
| A5 | Soak | 2 | TBD | TBD | TBD | TBD | TBD |

## Part B
1. A1-A5: the measured values are listed in the table above.
2. With 5 VUs, each iteration makes one HTTP request and then sleeps for one second. The full iteration also includes network response time, so each user completes fewer than one request per second; five users therefore produce less than 5 requests/second.
3. Compare A2 and A3 using the measured p(95) values. The tests use 3 and 5 VUs respectively, but both remain inside the small operational envelope permitted for the shared public demo. Whether latency grew must be stated from the recorded values, not assumed.
4. Compare the spike interval in A4's HTML report with the response-time series after load returns to 1 VU. Record the observed recovery time after the report is generated.
5. Compare the first and last minutes of A5 using its HTML report and the measured error rate. A multi-hour soak test can reveal resource leaks, such as a memory leak, that gradually increase latency or errors.
6. p(95) describes the slower tail of user requests; an average can hide a small but important group of very slow requests.
7. A lab system may have different CPU/memory and network latency from the public server; it may also have a different background workload or data volume.
8. Hundreds of VUs against a public service you do not own can overload it, degrade service for others, or be treated as abusive traffic. Load tests require ownership or explicit permission.
9. Vague requirement: "The app should load quickly." Testable example: "With 3 VUs for 30 seconds, 95% of product-search requests finish within 1 second, 99% within 1.5 seconds, and fewer than 1% fail." Example k6 thresholds: `http_req_duration: ['p(95)<1000', 'p(99)<1500']`, `http_req_failed: ['rate<0.01']`. Replace these examples with app-specific endpoints and realistic limits when testing an app you own.
