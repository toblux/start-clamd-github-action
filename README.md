# Start ClamAV Daemon GitHub Action

This GitHub action starts a lightweight ClamAV daemon. For now, `clamd` only loads the `bytecode.cvd` database.

On Linux and macOS, the server listens on TCP port 3310 and the Unix socket at `/tmp/clamd.socket`. On Windows, the server only listens on TCP port 3310.

## Usage

```yaml
name: Example workflow
on: [push, pull_request]

jobs:
  clamd_ubuntu:
    runs-on: ubuntu-latest
    steps:
      - name: Start ClamAV daemon clamd
        uses: toblux/start-clamd-github-action@main
      - name: Ping clamd on TCP port 3310
        run: echo PING | nc localhost 3310
      - name: Ping clamd using the Unix socket
        run: echo PING | nc -U /tmp/clamd.socket

  clamd_windows:
    runs-on: windows-latest
    steps:
      - name: Start ClamAV daemon clamd
        uses: toblux/start-clamd-github-action@main
      - name: Test the connection to clamd on TCP port 3310
        run: Test-NetConnection -ComputerName localhost -Port 3310
```
