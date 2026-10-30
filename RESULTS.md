# K6 lab results

Measurements below are from actual runs on this computer. Results vary because QuickPizza is a shared public service reached over the internet.

## Part 0
- Step 0.1: HTTP request returned 200; http_req_duration 264.83 ms.
- Step 0.2: 80 requests, 3.799693 requests/s, p(95)=284.67 ms. The rate is below 5 requests/s because each VU sleeps for one second and the iteration also includes network time.
- Step 0.6: default P95=1500 run exited 0 (p(95)=389.4 ms); P95=300 run exited 99 (measured p(95)=389.1 ms, so the threshold failed as expected).
- Step 0.7: normal thresholds passed; p(95)=396.61 ms and p(99)=410.11 ms. The negative test with P95=1 ms exited 99 as expected.
- Step 0.8: the bug was case-sensitive ingredient/tool names: lower-case 'pepperoni' and 'knife' did not match API names 'Pepperoni' and 'Knife'. Before the fix, checks passed 82.66% (66/75 for pepperoni and 45/75 for knife). After correcting capitalization, all 225 checks passed.

## Part A results
| Step | Test type | Max VUs | Requests | Req/s | p(95) | Max latency | Failed requests | Checks |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| A1 | Smoke | 1 | 15 | 0.458871 | 349.13 ms | 360.9 ms | 0.00% | 100% (20/20) |
| A2 | Average load | 3 | 240 | 1.29881 | 390.28 ms | 426.79 ms | 0.00% | 100% (320/320) |
| A3 | Stress | 5 | 399 | 2.199916 | 375.42 ms | 722.17 ms | 0.00% | 100% (532/532) |
| A4 | Spike | 5 | 150 | 1.057017 | 378.77 ms | 389.74 ms | 0.00% | 100% (200/200) |
| A5 | Soak | 2 | 651 | 0.985806 | 372.14 ms | 488.48 ms | 0.00% | 100% (868/868) |

## Part B
1. The smoke test passed all 20 checks. A2 passed all 320 checks; A3 passed all 532 checks; A4 passed all 200 checks; A5 passed all 868 checks. All five Part A runs had 0% failed HTTP requests.
2. With 5 VUs, the test makes one request per iteration and then sleeps for one second. Network response time is also part of the iteration, so the measured rate is lower than 5 requests/second.
3. A2 p(95) was 390.28 ms at 3 VUs; A3 p(95) was 375.42 ms at up to 5 VUs. In these runs, p(95) did not increase; network and shared-server variation may explain the small difference. The maximum observed latency did rise from 426.79 ms to 722.17 ms.
4. A4 reached 5 VUs briefly, then returned to 1 VU. Overall p(95) was 378.77 ms, maximum latency 389.74 ms, with 0% failed requests. Use the A4 HTML report's time series to inspect the response-time pattern during the spike and recovery.
5. A5 completed 10 minutes at 2 VUs with 651 requests, p(95)=372.14 ms, maximum latency 488.48 ms, 0% failed requests, and 100% checks (868/868). From the exported dashboard's 10-second snapshots, mean p(95) over the first minute was about 355.28 ms and over the last minute about 366.81 ms (an increase of 11.53 ms, about 3.2%). Both periods had 0% failed requests, so the run shows a small latency rise but no error-rate drift or obvious sustained degradation.
6. p(95) represents the 95th percentile of request duration and shows tail latency; an average can hide a small group of slow requests.
7. Local and public environments can differ in CPU, memory, network latency, background load, and data volume.
8. Sending hundreds of VUs to a public service without permission could overload it or degrade service for other users. Only test within the lab's limits or systems you own/are authorized to test.
9. Example testable requirement: "With 3 VUs for 30 seconds, 95% of product-search requests finish within 1 second, 99% within 1.5 seconds, and fewer than 1% fail." Example thresholds: `http_req_duration: ['p(95)<1000', 'p(99)<1500']` and `http_req_failed: ['rate<0.01']`. Adapt them to the actual app and agreed service-level targets.
