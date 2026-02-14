# Chapter 01 – Course Overview and Environment Setup

## Introduction to Tools in Data Science

In this session, the instructors introduced the philosophy behind the "Tools in Data Science" course. Unlike traditional subjects, this course focuses on "job readiness" and systems-level thinking. The goal is to move beyond writing simple code to building and deploying complex applications.

---

## Key Pillars of the Course

The instructors identified two critical concepts that determine success in this course and in the industry:

- **APIs (Application Programming Interfaces):** Understanding how to connect different services and data pipelines (the "plumbing" of software).
- **Deployment:** The ability to move code from a local machine to a publicly accessible server (Cloud, Docker, Serverless).

---

## What is WSL?

WSL (Windows Subsystem for Linux) was introduced as the primary development environment for Windows users in this course. It allows users to run a full Linux kernel inside Windows.

It provides:
- A native Linux environment without dual-booting.
- Seamless integration with VS Code.
- Support for essential tools like `uv`, `npx`, and `git`.

---

## Why Linux is Required?

- **Industry Standard:** Most real-world production servers run on Linux.
- **Tool Compatibility:** Many modern data science and development tools differ in behavior on Windows vs. Linux; using Linux ensures consistency.
- **Efficiency:** It is lightweight compared to traditional Virtual Machines (VMs) like Oracle VirtualBox.

---

## Ubuntu Setup & Prerequisites

Ubuntu is the recommended Linux distribution for this course. Before installation, users must ensure **Virtualization** is enabled in their BIOS and turn on "Virtual Machine Platform" in Windows Features.

In this session, setting up **Ubuntu (LTS version)** was demonstrated as the standard workflow.

---

## WSL Commands Explained

### `wsl --update`
Updates the WSL kernel to the latest version to ensure compatibility.

### `wsl --list --online`
Lists the available Linux distributions that are ready for download.

### `wsl --install`
Installs the default Linux distribution (usually the latest Ubuntu LTS).

### `sudo apt update && sudo apt upgrade`
Updates the list of available packages and installs the newest versions inside the Linux system.

---

## Importance of Environment Setup

This setup is the foundation for the entire term. Proper configuration ensures:
- can execute the course's "starter code" without errors.
- familiar with the Command Line Interface (CLI).
- ready for upcoming topics like Git version control and API development.
