# MyLast — Linux Authentication Log Analyzer

**A Bash-based command-line project for reconstructing Linux login sessions and examining failed authentication attempts from system logs.**

MyLast is a two-script implementation inspired by the Linux `last` and `lastb` utilities. Instead of reading `wtmp`/`btmp` databases, it parses `/var/log/auth.log` and rotated authentication logs, providing a practical exercise in **Linux system administration, Bash scripting, log parsing, and security-focused troubleshooting**.

## Features

- **Successful session analysis (`last.sh`)** — extracts login/session events and attempts to pair session starts with their corresponding ends.
- **Failed authentication analysis (`lastb.sh`)** — extracts PAM authentication failure records and displays users, authentication services, terminals, and timestamps.
- **Multiple authentication mechanisms** — handles selected SSH, `systemd-logind`, graphical greeter, and `su` session messages in the successful-session script.
- **Flexible CLI filtering** — restrict results by count, date/time criteria, and user; `lastb.sh` also supports terminal filtering.
- **Rotated log support** — processes regular and gzip-compressed authentication logs.

## Technologies and concepts

`Bash` · `Linux` · `PAM authentication logs` · `systemd-logind` · `SSH` · `grep` · `awk` · `sed` · `date` · `gzip` · `regular expressions`

The implementation uses Bash functions, indexed and associative arrays, process substitution, shell pipelines, command-line argument parsing, and timestamp conversion. Session starts and ends are correlated using identifiers extracted from log entries.

## Repository structure

```text
MyLast/
├── last.sh      # Parse successful login sessions
├── lastb.sh     # Parse failed authentication attempts
└── README.md    # Project documentation
```

## Getting started

### Requirements

- Linux (designed around Ubuntu/Debian-style `/var/log/auth.log` records)
- Bash and common GNU command-line utilities (`grep`, `awk`, `sed`, `date`, `gzip`, `tac`)
- Permission to read `/var/log/auth.log` and relevant rotated files

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
chmod +x last.sh lastb.sh
```

> Replace the placeholder repository URL and folder name with the actual GitHub repository. Depending on log permissions, running the scripts may require `sudo`.

## Usage

### 1. Inspect login sessions

```bash
./last.sh -n 5
./last.sh -s 2026-01-01
./last.sh -t 2026-01-31
./last.sh -n 10 alice
```

`last.sh` recognizes the following arguments:

| Option | Description |
| --- | --- |
| `-n NUMBER` | Maximum number of sessions to display |
| `-s DATE` | Filter log entries from the specified date/time onward |
| `-t DATE` | Filter log entries before the specified date/time |
| `-p DATE` | Restrict processing to a date-based window (see note below) |
| `USER` | Filter records by user-related text |

**Important:** The `-p` option in this implementation is a date-window filter; it does not fully reproduce the historical “sessions active at this exact moment” behavior of the standard `last` utility.

### 2. Inspect failed login attempts

```bash
./lastb.sh -n 10
./lastb.sh -s 2026-01-01 00:00:00
./lastb.sh -t 2026-01-31 23:59:59
./lastb.sh -p 2026-01-15 12:00:00
./lastb.sh alice tty3
```

`lastb.sh` recognizes the following arguments:

| Option | Description |
| --- | --- |
| `-n NUMBER` | Maximum number of matching failed authentication entries |
| `-s YYYY-MM-DD HH:MM:SS` | Only include failures after this timestamp |
| `-t YYYY-MM-DD HH:MM:SS` | Only include failures up to this timestamp |
| `-p YYYY-MM-DD HH:MM:SS` | Match an exact timestamp |
| `USER` | Filter by an existing local username |
| `TTY` | Filter by an existing terminal device |

**Note:** Date/time values for `lastb.sh` are supplied as two separate command-line arguments. The implementation validates the date and time format before processing.

## How it works

**`last.sh`** reads authentication log files, searches for recognized session-open and session-close events, and uses associative arrays to match certain events by their session or process identifier. It then formats each reconstructed record with a username, access method, start time, and either an end time or an indication that no end event was found.

**`lastb.sh`** reads current and rotated authentication logs, selects lines containing `authentication failure`, extracts user, service, terminal, and timestamp fields using regular expressions, applies user/time/terminal filters, and prints matching entries.

## Scope and limitations

This is an **educational log-analysis implementation**, not a drop-in replacement for Linux `last`/`lastb` and not a real-time intrusion-detection system.

- It parses authentication text logs rather than the `wtmp` and `btmp` databases used by the standard utilities.
- Results depend on the host's log format, log rotation configuration, available files, and file-read permissions.
- Session reconstruction supports selected message patterns; unrecognized or missing events may produce incomplete records.
- Timestamp handling and some CLI options differ between the two scripts and from the original utilities.
- The scripts have been checked for Bash syntax, but an end-to-end runtime test with representative system logs is not included in this repository.

## Contributors

Developed as a team project by **Eliza-Georgiana Boroș** and **Rebeca Nicula**.

## Skills demonstrated

- Parsing and filtering Linux authentication logs with Bash
- Working with Unix command-line tools and compressed/rotated files
- Reconstructing session information from event-oriented records
- Designing configurable command-line utilities
- Handling input validation and time-based filtering
