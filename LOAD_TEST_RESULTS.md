
# Load Test Results

## Test 1: Normal Load (100 Users)

### Test Configuration
- Number of Threads (Users): 100
- Ramp-up Period: 10 seconds
- Loop Count: 1
- Same user on each iteration: Enabled
- Duration: 120 seconds

### Summary Statistics
- Total Samples: 330
- Failures: 0
- Error %: 0.00%
- Average Response Time: 9.10 ms
- 90th Percentile: 16 ms
- Throughput: 34.52 TPS

Key Observations:
- Excellent performance
- No failures
- All endpoints within acceptable limits

---

## Test 2: High Load (2050 Users)

### Test Configuration
- Users: 2050
- Ramp-up: 1 second
- Duration: 120 seconds

### Summary
- Total Samples: 4716
- Failures: 0
- Avg Response Time: 5296.53 ms
- 90th Percentile: 16241 ms
- Throughput: 212.78 TPS

Observations:
- Significant response delay
- Token and List endpoints most impacted
- No errors, but performance degradation visible

---

## Test 3: Very High Load (2100 Users)

### Test Configuration
- Users: 2100
- Ramp-up: 1 second
- Duration: 120 seconds

### Summary
- Total Samples: 4831
- Failures: 6
- Error Rate: 0.12%
- Avg Response Time: 5771.59 ms
- 90th Percentile: 18594 ms
- Throughput: 202.92 TPS

Observations:
- System threshold breached
- Failures observed in Create and Update endpoints
- Very high latency in List All Books and Create Book

---

## Final Conclusion

✅ System performs optimally up to 100 users  
⚠️ Performance degrades significantly after 2000 users  
🚨 2100 users causes failures and SLA breaches  

Recommended Actions:
- Optimize List and Create APIs
- Introduce caching for read-heavy endpoints
- Apply rate limiting or autoscaling
