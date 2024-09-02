# 5G Network Slice Security Tester

RingFencingTester is a comprehensive testing framework designed to evaluate the performance of ring fencing appliances in 5G Core Networks. It simulates PFCP (Packet Forwarding Control Protocol) traffic, applies ring fencing rules, and measures various performance metrics in compliance with 3GPP specifications.

# Detailed Features of 5G Network Slice Security Tester

1. Configurable Network Slice Simulation
   - Supports eMBB, URLLC, and mMTC slice types as defined in 3GPP TS 23.501 Section 5.15 (Network Slicing)
   - Allows custom configuration of slice parameters (e.g., traffic load, security policies)
       - config/default_config.yaml: Defines slice configurations
       - src/tester/slice_security_tester.py: Orchestrates slice-specific testing
   - Aligns with Network Slice Selection Assistance Information (NSSAI) concept (3GPP TS 23.501 Section 5.15.2)

2. PFCP (Packet Forwarding Control Protocol) Traffic Generation
   - Implements PFCP as specified in 3GPP TS 29.244 (Interface between the Control Plane and the User Plane of EPC Nodes)
       - src/generators/pfcp_generator.py: Implements PFCP packet generation
       - src/generators/traffic_generator.py: Uses PFCP generator to create slice-specific traffic
   - Generates realistic 5G core network traffic patterns
   - Supports various PFCP message types (e.g., Session Establishment, Modification, Deletion)

3. Ring Fencing Rule Application and Testing
   - Applies isolation mechanisms as described in 3GPP TS 23.501 Section 5.15.2.2 (Network Slice Instance Isolation)
   - Tests data flow isolation between network slices
       - src/tester/ring_fencing_tester.py: Applies and tests ring fencing rules
   - Simulates differentiated slice behaviors based on 3GPP TS 23.501 Section 5.15.2.3

4. Comprehensive Security Analysis
   - Analyzes slice isolation effectiveness (3GPP TS 33.501 Section 5.9) (Security Architecture and Procedures for 5G System)
   - Checks encryption mechanisms (3GPP TS 33.501 Section 6.2)
   - Verifies authentication procedures (3GPP TS 33.501 Section 6.1)
   - Detects potential vulnerabilities in slice implementation
       - src/analyzers/security_analyzer.py: Performs security analysis on generated traffic

5. Detailed Performance Metrics Calculation
   - Measures throughput in alignment with 3GPP TS 28.552(Management and orchestration; 5G performance measurements) Section 5.1.1.3.1
   - Calculates latency as per 3GPP TS 28.552 Section 5.1.1.3.2
   - Assesses packet loss rate (3GPP TS 28.552 Section 5.1.1.3.3)
   - Evaluates jitter, relevant for URLLC services (3GPP TR 38.824)
   - src/analyzers/performance_analyzer.py: Calculates performance metrics for each slice

6. Extensible Architecture
   - Modular design allows easy integration of new test scenarios. Not directly tied to a specific 3GPP standard, but aligns with the modular nature of 5G architecture
   - Supports addition of new network functions as defined in 3GPP TS 23.501 Section 6
   - Facilitates testing of evolving 5G features and capabilities
   - Code Implementation:
     - Overall project structure allows easy addition of new modules
     - src/tester/base_tester.py: Provides a base class for creating new test types

7. Detailed Logging and Error Handling
   - Provides comprehensive logging of test procedures and results
   - Implements robust error handling to ensure test reliability
   - Aids in troubleshooting and debugging of network slice issues

8. Configurable Test Parameters via YAML
   - Allows flexible configuration of test scenarios
   - Supports definition of slice-specific parameters as per 3GPP TS 28.541 (Management and orchestration; 5G Network Resource Model) Section 6.3
   - Enables easy customization for different network environments and test cases
   - config/default_config.yaml: Main configuration file

9.  Generation of Detailed and Summary Reports
   - Produces comprehensive reports on security and performance metrics
   - Aligns with KPI reporting as per TS 28.554 (Management and orchestration; 5G End to end Key Performance Indicators)
   - Facilitates analysis and optimization of network slice performance
   - src/utils/report_generator.py: Generates comprehensive test reports

10. QoS Aware Testing
    - Incorporates QoS flow handling as specified in 3GPP TS 23.501 Section 5.7
    - Tests differentiated treatment of traffic based on 5QI (5G QoS Identifier)
        - QoS parameters in config/default_config.yaml
        - QoS-aware traffic generation in src/generators/traffic_generator.py
    - Evaluates QoS enforcement in line with 3GPP TS 23.503

11. Service-Based Interface Testing
    - Simulates interactions between network functions using service-based interfaces (3GPP TS 23.501 Section 4.2.6)
    - Tests service registration and discovery processes
    - Aligns with the Service-Based Architecture (SBA) principles of 5G

12. Network Exposure Function (NEF) Simulation
    - Implements NEF functionality as defined in 3GPP TS 23.502 Section 5.2.6
        - Placeholder for NEF functionality in src/tester/slice_security_tester.py
    - Supports testing of network capability exposure to external applications
    - Evaluates security aspects of network exposure (3GPP TS 33.501 Section 12)

13. Edge Computing Scenario Testing
    - Supports testing of Multi-access Edge Computing (MEC) scenarios
        - Placeholder for edge scenario testing in src/tester/slice_security_tester.py
    - Aligns with 3GPP TR 23.748 for 5G enhancement for edge computing
    - Evaluates performance metrics specific to edge deployment scenarios

14. Network Data Analytics Function (NWDAF) Integration
    - Incorporates NWDAF as specified in 3GPP TS 23.288
    - Simulates collection and analysis of network data
    - Tests data-driven optimization and slice management scenarios
        - Placeholder for NWDAF functionality in src/analyzers/performance_analyzer.py

15. Time-Sensitive Networking (TSN) Support
    - Implements TSN support as defined in 3GPP TS 23.501 Section 5.27
    - Tests integration of 5G system with TSN networks
        - TSN parameters in config/default_config.yaml
        - Placeholder for TSN testing in src/tester/slice_security_tester.py
    - Evaluates performance for time-sensitive communications

Each of these features is designed to provide comprehensive testing and validation of 5G network slice implementations, ensuring alignment with 3GPP standards and specifications. The tester's capabilities cover a wide range of aspects critical to the successful deployment and operation of 5G network slices, from basic connectivity and performance to advanced features like edge computing and time-sensitive networking.


## Prerequisites

- Python 3.7+
- Scapy library
- Access to a 5G Core Network environment or simulator

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/cem8kaya/RingFencingTester.git
   ```

2. Navigate to the project directory:
   ```
   cd RingFencingTester
   ```

3. Install required dependencies:
   ```
   pip install -r requirements.txt
   ```

## Usage

1. Configure the test parameters in `config.py`:

   ```python
   config = {
       "src_ip": "192.0.2.1",
       "dst_ip": "192.0.2.2",
       "duration": 300,
       "num_packet_pairs": 1000,
       "output_pcap": "5g_ringfence_test_traffic.pcap",
       "ring_fencing_rules": [
           {"type": "block", "protocol": "udp", "port": 8805},
           {"type": "allow", "ip_range": "192.0.2.0/24"},
           {"type": "rate_limit", "traffic_type": "non-GBR", "max_rate": "10Mbps"}
       ],
       "performance_thresholds": {
           "max_latency": 50,
           "min_throughput": 1000,
           "max_packet_loss": 0.1
       },
       "network_slices": [
           {"type": "eMBB", "traffic_load": 1000},
           {"type": "URLLC", "traffic_load": 500},
           {"type": "mMTC", "traffic_load": 10000}
       ]
   }
   ```

2. Run the tester:

   ```
   python RingFencingTester.py
   ```

3. View the generated reports in the `reports` directory.

## Test Scenarios

The RingFencingTester supports various test scenarios, including:

- Basic PFCP traffic testing
- Network slice-specific testing (eMBB, URLLC, mMTC)
- QoS flow testing
- Mobility scenarios
- Edge computing scenarios

Refer to the `scenarios.md` file for detailed information on each test scenario and how to configure them.

## Extending the Tester

To add new test scenarios or enhance existing functionality:

1. Create a new class that inherits from `RingFencingTester` or `EnhancedRingFencingTester`.
2. Implement new methods for specific test cases or metrics.
3. Update the `run_test` method to include your new scenarios.
4. Modify the report generation to include new metrics or results.

Example:

```python
class CustomRingFencingTester(EnhancedRingFencingTester):
    def __init__(self, config):
        super().__init__(config)
        self.custom_metric = 0

    def custom_test_scenario(self):
        # Implement your custom test scenario
        pass

    def run_test(self):
        super().run_test()
        self.custom_test_scenario()
        self.generate_custom_report()

    def generate_custom_report(self):
        # Generate a report with custom metrics
        pass
```

## Contributing

Contributions to RingFencingTester are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them with descriptive commit messages.
4. Push your changes to your fork.
5. Submit a pull request to the main repository.

Please ensure your code adheres to the project's coding standards and includes appropriate tests and documentation.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions, issues, or suggestions, please open an issue on the GitHub repository or contact the maintainers at [cem8kaya@gmail.com](mailto:cem8kaya@gmail.com).

## Acknowledgments

- 3GPP for providing the specifications and standards for 5G networks.
- The Scapy project for the powerful packet manipulation library.
- Contributors and maintainers of open-source 5G Core Network simulators and tools.
