# Start ClamAV Daemon GitHub Action

This GitHub action starts a lightweight ClamAV daemon. By default, `clamd` loads only the `bytecode` database, but the `main` and `daily` databases can be enabled if needed.

The action works on Linux, macOS, and Windows runners. On Linux and macOS, `clamd` listens on TCP port 3310 and the Unix socket at `/tmp/clamd.socket`. On Windows, `clamd` listens on TCP port 3310.

## Inputs

No inputs are required for this action to run. Please refer to [action.yml](action.yml) to see which inputs can be customized and their default values.

## Usage

```yaml
name: Example workflow
on: [push, pull_request]
jobs:
  clamd_ubuntu:
    runs-on: ubuntu-latest
    steps:
      - name: Start ClamAV daemon clamd
        uses: toblux/start-clamd-github-action@v0.2.1
        with: # Custom inputs are optional (these are the default values)
          unix_socket: /tmp/clamd.socket
          tcp_port: 3310
          stream_max_length: 1M
      - name: Ping clamd on TCP port 3310
        run: echo PING | nc localhost 3310
      - name: Ping clamd using the Unix socket
        run: echo PING | nc -U /tmp/clamd.socket
  clamd_windows:
    runs-on: windows-latest
    steps:
      - name: Start ClamAV daemon clamd
        uses: toblux/start-clamd-github-action@v0.2.1
      - name: Test the connection to clamd on TCP port 3310
        run: Test-NetConnection -ComputerName localhost -Port 3310
```
