---
theme: default
title: Welcome to Devcon
---

# Streamlining Development with CI/CD

## Benefits and Best Practices

## Fu Hanxi

---

# Contents

- How we do CI/CD internally?
- Tools we developed for CI/CD
- How to use CI/CD in your project?
- What else can CI/CD do while releasing?

---

# Overview of Our Internal CI/CD Process

<img src="images/internal-process.svg">

---

# Difficulties we were Facing

- Support multiple targets
- Support multiple configurations
- Interact with multiple serial devices
- Support multiple OS and platforms


---

# Tools We Developed for CI/CD

- `idf-build-apps`

    A tool to build multiple ESP-IDF applications simply in CI

    - Repo: https://github.com/espressif/idf-build-apps
    - Documentation: https://docs.espressif.com/projects/idf-build-apps/en/latest/

- `pytest-embedded`

    A pytest plugin that designed for embedded testing

    - Repo: https://github.com/espressif/pytest-embedded
    - Documentation: https://docs.espressif.com/projects/pytest-embedded/en/latest/

---

# `idf-build-apps`

<img src="images/build-process.svg">

- Project
- Configuration
- Target
- Application

---

## Key Features

- Build matrix for multiple targets and configurations
- Manifest file for fine-grained control over the build matrix
- Skip build if the app is not modified, or the dependencies are not changed

---

# `pytest-embedded`

<img src="images/pytest-process.svg">

---

## Key Features

- Support all operating systems and platforms
- Run on different platforms without any code change
- Automatically setup firmware while setup

---

# Same Script, Different Platform​

```python
# test_hello_world.py
from pytest_embedded_idf import IdfDut

def test_hello_world(dut: IdfDut):
    dut.expect("Hello World!")
```

## Test ESP-IDF Project on Real Target

```shell
pytest --embedded-services esp,idf
```

## Test arduino-esp32 Project

```shell
pytest --embedded-services esp,arduino
```

## Test ESP-IDF Project with QEMU

```shell
pytest --embedded-services idf,qemu
```

---

# How to use CI/CD in your project?

<img src="images/release-process.svg">

---

# Different Platforms

## Test with Real Targets

Self-hosted runners on GitHub Actions - https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners

## Test with QEMU

Qemu is still under beta testing, but you can try it now.

- https://github.com/hfudev/devcon
- https://hub.docker.com/r/hfudev/qemu


---

# Demo with GitHub Actions

<img src="images/pipeline.svg">

---

# What Else Can CI/CD Do?

- Sign Your App with HSM
  - https://docs.espressif.com/projects/esptool/en/latest/esp32s2/espsecure/index.html#remote-signing-using-an-external-hsm
- Deploy Your App with esp-insights (beta)
  - https://github.com/espressif/esp-insights
- Generate Software Bill of Materials (beta)
  - https://github.com/espressif/esp-idf-sbom

---

# Thanks for Watching!
