#.Site: HUMAIN's first building — 50 MW, 18,000 NVIDIA GB300 GPUs

## 1. How many racks and GPUs does the site's power buy?

Starting from 50 MW:
50 × 0.8 = 40 MW
40 ÷ 1.25 = 32 MW of IT power
32 × 0.9 = 28.8 MW for compute
A GB300 NVL72 rack draws about 120 kW and holds 72 GPUs.
28,800 ÷ 120 = 240 racks
240 × 72 = 17,280 GPUs
The announced figure is 18,000, so our arithmetic agrees within about 4%.
> **240 racks and 17,280 GPUs.**


## 2. What is the largest open model it can serve, and how many copies?

Total site memory:
240 × 20 TB = 4,800 TB
= 4.8 × 10¹⁵ bytes
At fp8:
1 byte per parameter
4.8 × 10¹⁵ bytes
= 4,800 trillion parameters
= 4.8 quadrillion parameters
> **Largest model ≈ 4.8 quadrillion parameters.
> Number of copies = 1 **
> **Assumption I calculated the model weights only because there is not enough information for the KV cache. **

## 3. What is the largest model it could train in six months?

Using the 17,280 GPUs from Q1, with H100's peak TFLOPS as a stand-in:
989 × 0.40 = 395.6 TFLOPS per GPU
17,280 × 395.6
= 6,835,968 TFLOPS
= 6.836 × 10¹⁸ FLOPS/s
6 months = 15,552,000 seconds
6.836 × 10¹⁸ × 15,552,000
≈ 1.06 × 10²⁶ FLOPs
Training FLOPs:
6 × N × 20N
= 120N²
1.06 × 10²⁶ ÷ 120
≈ 8.87 × 10²³
N ≈ 942 billion parameters
Training tokens:
942B × 20
≈ 18.8T tokens
 > **Largest model ≈ 942B parameters
Training tokens ≈ 18.8T **
> ** Assumption I used H100's 989 TFLOPS because the case does not give a GB300 figure. **


## 4. What is its electricity bill for a month?

50 × 0.65 = 32.5 MW
32.5 × 720
= 23,400 MWh
23,400 × 1,000
= 23,400,000 kWh
Commercial rate:
23,400,000 × $0.08
= $1,872,000
Industrial rate:
23,400,000 × $0.048
= $1,123,200
> **Commercial rate = $1.872M/month
Industrial rate = $1.1232M/month **



## 5. What does a million tokens cost, at 30% and at 80% of capacity sold?

Monthly cost:
50 × $450,000
= $22.5M
$22.5M + $1.872M
= $24.372M/month
Max monthly output:
17,280 × 125 × 2,592,000
≈ 5.6T tokens/month
30% capacity:
5.6T × 0.30
= 1.68T tokens
$24.372M ÷ 1,679,616
≈ $14.51 per 1M tokens
80% capacity:
5.6T × 0.80
= 4.48T tokens
$24.372M ÷ 4,478,976
≈ $5.44 per 1M tokens
> **30% = $14.51 per 1M tokens
80% = $5.44 per 1M tokens **

##. Assumptions
- I used H100's 989 TFLOPS because the case does not give a GB300 figure.
- For Q2, I calculated the model weights only because there is not enough information for the KV cache.
- I assumed the monthly cost stays the same at different utilization levels.
- I used the 17,280 GPUs from Q1 for the other calculations. 
