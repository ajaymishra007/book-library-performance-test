# Book Library API Tests

This repository contains automated performance and reliability tests for the **Book Library API** using **Apache JMeter**. The project is structured to support multiple test types such as Load, Spike, and Chaos testing, with Docker-based execution for consistency and portability.

---

## 📁 Project Structure

```
book-library-jmeter-tests/
├── .github/
├── docker/
│   └── Dockerfile.jmeter
├── jmx/
│   ├── chaos_test.jmx
│   ├── load_test.jmx
│   ├── spike_test_concurrency_thread_group.jmx
│   └── spike_test_ultimate_thread_group.jmx
├── plugins/
│   ├── ext/
│   │   ├── jmeter-plugins-casutg-2.10.jar
│   │   └── jmeter-plugins-manager-1.6.jar
│   └── lib/
│       └── jmeter-plugins-cmn-jmeter-0.6.jar
├── reports/
├── screenshots/
├── docker-compose-chaos.yml
├── docker-compose-load.yml
├── docker-compose-spike-concurrency.yml
├── docker-compose-spike-ultimate.yml
├── LOAD_TEST_RESULTS.md
├── SPIKE_TEST_RESULTS.md
└── README.md
```

---

## ✅ Setup

### Prerequisites

Ensure the following are installed:
- Docker
- Docker Compose
- Git
- Java 8 or above

### Installation Steps

1. Clone the repository:
```bash
  git repo url: https://github.com/ajaymishra007/book-library-performance-test.git

cd book-library-jmeter-tests
```

2. No local JMeter installation is required. All dependencies are packaged inside Docker using the custom JMeter image defined in:
```
  docker/Dockerfile.jmeter
```

3. JMeter plugins are pre-bundled in the `plugins/` directory and copied into the container during build.

---

## ▶️ Running Tests


### 🖥️ Running Tests via Docker

All test executions are containerized. Use the following commands based on test type.

### Load Test
```bash
  docker-compose -f docker-compose-load.yml up --build
```

### Spike Test (Concurrency Thread Group)
```bash
  docker-compose -f docker-compose-spike-concurrency.yml up --build
```

### Spike Test (Ultimate Thread Group)
```bash
  docker-compose -f docker-compose-spike-ultimate.yml up --build
```

### Chaos Test
```bash
  docker-compose -f docker-compose-chaos.yml up --build
```

Test results (JTL, reports, logs) will be generated inside the `reports/` directory.

---

### 🖥️ Running Tests via JMeter GUI

If you prefer executing tests in JMeter's graphical interface for debugging or analysis, follow these steps:

#### Prerequisites
- Apache JMeter installed locally
- Java 8 or above

#### Steps

1. Download and install Apache JMeter from:
   https://jmeter.apache.org/download_jmeter.cgi

2. Make sure to install Jmeter 5.5.0 or above and copy and paste the jars present under `plugins/` folder attached in this project, in the respective folders in apache-jemeter-5.5 folder, where it is downloaded. After running Jmeter GUI, File>open> Open respective JMX file and run

3. Navigate to the `jmx/` folder in this project.

4. Launch JMeter:

   **Windows:**
   ```bash
   jmeter.bat
   ```

   **Mac / Linux:**
   ```bash
   ./jmeter
   ```

5. In JMeter GUI:
    - Click **File → Open**
    - Select one of the test plans:
        - `load_test.jmx`
        - `spike_test_concurrency_thread_group.jmx`
        - `spike_test_ultimate_thread_group.jmx`
        - `chaos_test.jmx`

6. Update parameters if needed:
    - Base URL
    - Thread count
    - Ramp-up time
    - Assertions

7. Click ▶️ **Start** to execute the test.

8. View live results in:
    - View Results Tree
    - Summary Report
    - Aggregate Report

> ⚠️ Note: GUI mode is recommended for test design and debugging only. For performance benchmarks and large load, always use **non-GUI (Docker) mode**.

---
## 🧠 Design Decisions

- **Dockerized Execution**  
  Ensures consistent environment setup across machines, removing dependency on local JMeter versions or plugin installations.

- **Separate JMX per Test Type**  
  Each performance strategy (Load, Spike, Chaos) has its own JMX file to maintain clear isolation, reusability, and easier tuning.

- **Pre-bundled Plugins**  
  Using JMeter Plugins Manager and custom thread groups (CASUTG, Ultimate TG) allows advanced load modeling without runtime installations.

- **Compose-based Orchestration**  
  Docker Compose files provide simple, repeatable commands for each scenario, improving usability for QA and DevOps users.

- **Results Documentation**  
  Test outcomes are documented in:
  - `LOAD_TEST_RESULTS.md`
  - `SPIKE_TEST_RESULTS.md`
  
  This helps in tracking performance trends and reporting.

---

## 🚀 What's Next

With more time, the following enhancements would be added:

- ✅ Allure or HTML Dashboard integration for rich visual reporting
- ✅ CI/CD integration (GitHub Actions / Jenkins) for automated performance testing
- ✅ Parameterization via external CSV and environment configs
- ✅ Threshold-based assertions and SLA validation
- ✅ Grafana + InfluxDB integration for real-time performance monitoring
- ✅ Dynamic test execution via command-line arguments
- ✅ Automatic comparison between test runs

---

## 📌 Notes

- Ensure target Book Library API service is running and accessible before executing tests.
- Modify base URL and credentials inside JMX files if environment changes.

---

📞 For any updates or enhancements, feel free to extend this README as the project evolves.

