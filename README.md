# cast

Minimal SSH deploy tool in ~150 lines of POSIX shell.

## Features

- Single file, zero dependencies
- Declarative `Castfile` syntax
- Dry-run mode
- Multi-host support
- File copying and remote command execution

## Usage

```sh
cast [options] <task>

Options:
  -f <file>    Castfile path (default: ./Castfile)
  -h <host>    Override host (user@host)
  -n           Dry run (print commands only)
  -v           Verbose output
```

## Castfile Example

```
host web user@192.168.1.10
host db user@192.168.1.20

ssh_opts -i ~/.ssh/id_ed25519

task deploy
  run mkdir -p /opt/app
  copy ./app /opt/app/app
  run chmod +x /opt/app/app
  run systemctl restart app

task status
  run systemctl status app
  run journalctl -u app --no-pager -n 20
```

## Install

```sh
curl -sL https://3-n.lain.ch/git/cast/plain/cast > /usr/local/bin/cast
chmod +x /usr/local/bin/cast
```

## License

MIT
