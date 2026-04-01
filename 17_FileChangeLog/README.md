# FileChangeLog

Monitor a given directory (specified via --dir) for any file system changes and append each detected event with a timestamp to a log file.

## What It Does

Watches a user-specified directory for file creation, modification, and deletion events. Each event is timestamped and appended to `changelog.log`, while also being printed to the console.

## Features Tested

- **Command-line parameters** - `--dir` to specify the watched directory
- **File monitoring** - `Start` action with `file-monitor`
- **File event handlers** - `File Event Handler` business activity pattern
- **Timestamps** - `<now>` for current UTC time in log entries
- **File append** - `Append` action to write to the log file
- **String interpolation** - Building log entries with `${<var>}` syntax
- **Keepalive** - Long-running application with graceful shutdown

## Related Proposals

- [ARO-0008: I/O Services](../../Proposals/ARO-0008-io-services.md)
- [ARO-0036: File Operations](../../Proposals/ARO-0036-file-operations.md)
- [ARO-0047: Command-Line Parameters](../../Proposals/ARO-0047-command-line-parameters.md)

## Prompt

> Monitor a given directory (specified via --dir) for any file system changes and append each detected event with a timestamp to a log file.

## Usage

```bash
# Watch a specific directory
aro run ./Examples/17_FileChangeLog --dir /tmp/watched

# In another terminal, trigger some changes
touch /tmp/watched/test.txt
echo "hello" >> /tmp/watched/test.txt
rm /tmp/watched/test.txt

# Press Ctrl+C to stop
```

## Example Output

```
Monitoring /tmp/watched for changes...
Writing events to changelog.log
[2026-04-01T12:00:00Z] CREATED /tmp/watched/test.txt
[2026-04-01T12:00:01Z] MODIFIED /tmp/watched/test.txt
[2026-04-01T12:00:02Z] DELETED /tmp/watched/test.txt
^C
File change log stopped.
```

## Log File Format

Each line in `changelog.log` follows the format:

```
[<ISO-8601 timestamp>] <EVENT_TYPE> <file_path>
```

---

*Never miss a change. Every file event, timestamped and logged.*
