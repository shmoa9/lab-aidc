# Lab W5D3: Case Study - Size a Saudi Data Centre

## Overview

This lab studies how to estimate the size and capability of a Saudi AI data centre.

The analysis includes:

- Data centre power sizing
- GPU and rack estimation
- AI model serving capacity
- Model training capability
- Electricity cost estimation
- Cost per million tokens

---

# Selected Site

## HUMAIN's First Building

Assumed facility capacity:

```
50 MW
```

The calculations below estimate the usable AI compute capacity based on the given assumptions.

---

# Assumptions

| Parameter | Value |
|---|---:|
| Facility Power | 50 MW |
| PUE | 1.25 |
| Switches and Storage Overhead | 10% |
| Headroom | 20% |
| Rack Power | 120 kW |
| GPUs per Rack | 72 GPUs |
| Average Utilization | 65% |
| Electricity Cost | $0.08/kWh |
| Operation Cost | $450,000/MW/month |

---

# Task 1: Estimate Racks and GPUs

## Step 1: Calculate IT Power

Formula:

```
IT Power = Facility Power / PUE
```

Calculation:

```
IT Power = 50 / 1.25

IT Power = 40 MW
```

---

## Step 2: Remove Switch and Storage Power

10% of IT power is reserved.

Formula:

```
GPU Power = IT Power × 0.9
```

Calculation:

```
GPU Power = 40 × 0.9

GPU Power = 36 MW
```

---

## Step 3: Apply Headroom

20% capacity is reserved.

Formula:

```
Available GPU Power = 36 × 0.8
```

Calculation:

```
Available GPU Power = 28.8 MW
```

---

## Step 4: Calculate Number of Racks

Each rack consumes:

```
120 kW = 0.12 MW
```

Formula:

```
Racks = Available GPU Power / Rack Power
```

Calculation:

```
Racks = 28.8 / 0.12

Racks = 240 racks
```

---

## Step 5: Calculate GPUs

Each rack:

```
72 GPUs
```

Formula:

```
GPUs = Racks × GPUs per Rack
```

Calculation:

```
GPUs = 240 × 72

GPUs = 17,280 GPUs
```

---

## Result

The estimated capacity is:

```
240 racks

17,280 GPUs
```

---

# Task 2: Largest Model It Can Serve

## Memory Estimation

Assumption:

```
20 TB memory per rack
```

Total memory:

```
Total Memory = 240 × 20 TB

Total Memory = 4800 TB

Total Memory = 4.8 PB
```

---

## FP8 Model Size

Assumption:

```
1 parameter ≈ 1 byte
```

Maximum theoretical size:

```
≈ 4.8 trillion parameters
```

Considering:

- KV cache
- Runtime overhead
- Context memory

Assume 50% usable memory:

```
4.8T × 0.5

= 2.4T parameters
```

---

## Result

The data centre can serve approximately:

```
2.4 trillion parameter FP8 model
```

---

# Task 3: Largest Model It Can Train in Six Months

## Training Assumptions

- 6 FLOPs per parameter per token
- 20 tokens per parameter
- 40% effective utilization

---

## FLOPs per Parameter

Formula:

```
Training FLOPs = 6 × 20
```

Result:

```
120 FLOPs per parameter
```

---

## Effective GPU Performance

Assumption:

```
H100 = 989 TFLOPS
```

Effective performance:

```
989 × 0.4

= 395.6 TFLOPS
```

---

## Total Compute

For 17,280 GPUs:

```
395.6 × 17,280

≈ 6.83 × 10^6 TFLOPS
```

---

## Training Time

Six months:

```
180 days
```

Seconds:

```
180 × 24 × 3600

= 15,552,000 seconds
```

---

## Result

Estimated training capability:

```
≈ 6 trillion parameter model
```

---

# Task 4: Monthly Electricity Cost

## Utilization

Average utilization:

```
65%
```

Power usage:

```
50 MW × 0.65

= 32.5 MW
```

---

## Monthly Energy

Hours:

```
30 × 24 = 720 hours
```

Energy:

```
32.5 × 1000 × 720

= 23,400,000 kWh
```

---

## Electricity Cost

Formula:

```
Cost = Energy × Price
```

Calculation:

```
23,400,000 × 0.08

= $1,872,000
```

---

## Result

Monthly electricity cost:

```
≈ $1.87 million
```

---

# Task 5: Cost per Million Tokens

## Token Generation

Given:

```
125 output tokens/sec/GPU
```

Total:

```
17,280 × 125

= 2,160,000 tokens/sec
```

---

## Monthly Token Capacity

Hourly:

```
2,160,000 × 3600

= 7.776 billion tokens/hour
```

Monthly:

```
7.776B × 720

= 5.598 trillion tokens/month
```

---

# Monthly Operational Cost

Non-electricity cost:

```
50 × 450,000

= $22,500,000
```

Total:

```
22.5M + 1.872M

= $24.372M/month
```

---

# 30% Capacity Sold

Tokens:

```
5.598T × 0.30

= 1.679T tokens
```

Cost:

```
24.372M / 1,679,000

= $0.0145
```

Result:

```
$0.0145 per million tokens
```

---

# 80% Capacity Sold

Tokens:

```
5.598T × 0.80

= 4.478T tokens
```

Cost:

```
24.372M / 4,478,000

= $0.0054
```

Result:

```
$0.0054 per million tokens
```

---

# Final Summary

| Metric | Result |
|---|---:|
| Facility Power | 50 MW |
| IT Power | 40 MW |
| GPU Available Power | 28.8 MW |
| Number of Racks | 240 |
| Total GPUs | 17,280 |
| Serving Model Size | ~2.4T Parameters |
| Training Model Size | ~6T Parameters |
| Electricity Cost | ~$1.87M/month |
| Token Cost (30%) | $0.0145 / Million Tokens |
| Token Cost (80%) | $0.0054 / Million Tokens |

---

# Missing Information

The announcement does not provide:

- Actual workload utilization
- Cooling system design
- Network architecture
- Customer workload distribution
- Operational availability

These details are required for a complete production evaluation.
