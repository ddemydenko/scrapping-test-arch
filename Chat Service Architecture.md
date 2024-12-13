
# WebSocket Scaling on AWS EC2 and ALB

This project demonstrates the scalability of WebSocket connections on AWS infrastructure and provides insights into effective scaling strategies.

## WebSocket Connections on EC2 t3.medium

### Estimated Capacity
- **t3.medium Specifications**:
    - 4 GB RAM
    - 2 vCPU
    - Up to 5 Gbps network bandwidth

- **Memory Considerations**:  
  On a t3.medium instance, approximately 3.5 GB of memory is available for WebSocket connections after accounting for the Node.js runtime and other system processes (~0.5 GB reserved).
    - Each WebSocket connection consumes approximately 64 KB of memory under typical conditions (minimal payloads, efficient buffers).
    - Using these assumptions:  
      Max Connections = Available Memory / Memory per Connection  
      Max Connections = 3.5 GB / 64 KB ≈ 56,000 connections

- **Practical Adjustments**:  
  In practice, factors like additional libraries, larger message buffers, or spikes in CPU usage may reduce the total capacity to 30,000 - 40,000 connections for a stable WebSocket chat application.

### Resource Limitations
- **CPU**: While memory is the primary constraint for WebSocket connections, CPU may become a limiting factor with frequent message exchanges or complex application logic.
- **Network Bandwidth**: With 5 Gbps bandwidth, the t3.medium can support tens of thousands of connections assuming typical message sizes for a text-based chat application (~200 bytes/message).

---

## Scaling WebSocket Applications

To ensure your WebSocket service scales effectively with increasing demands, leverage AWS Application Load Balancer (ALB) and Amazon ECS auto-scaling capabilities.

### Key Metrics for Scaling
1. **ActiveConnectionCount**
    - Monitors the total number of active WebSocket connections managed by the ALB.
    - Enables dynamic scaling of ECS tasks or EC2 instances based on the number of concurrent connections.

2. **TargetResponseTime**
    - Tracks the average response time of ECS tasks or EC2 instances behind the ALB.
    - Triggers scaling actions when latency exceeds predefined thresholds, ensuring consistent performance.

### Scaling Recommendations
- Use **Target Tracking Scaling Policies** in ECS:
    - For ActiveConnectionCount, set thresholds based on the estimated connection capacity of your EC2 instances or ECS tasks.
    - For TargetResponseTime, define acceptable latency limits (e.g., 500 ms) to maintain responsiveness.

- Monitor and analyze these metrics using **Amazon CloudWatch** to refine scaling policies over time.
