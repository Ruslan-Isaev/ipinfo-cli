# ipinfo

A minimal Bash utility for querying IP address information from the command line using the [ipwho.is](https://ipwho.is) API.

## Usage

```bash
ipinfo <ip>
```

**Example:**

```bash
ipinfo 8.8.8.8
```

**Output** (pretty-printed JSON):

```json
{
  "ip": "8.8.8.8",
  "success": true,
  "type": "IPv4",
  "country": "United States",
  "country_code": "US",
  "city": "Mountain View",
  "latitude": 37.4056,
  "longitude": -122.0775,
  "isp": "Google LLC",
  ...
}
```

## Requirements

- `bash`
- [`curl`](https://curl.se/)
- [`jq`](https://stedolan.github.io/jq/)

Install `jq` if needed:

```bash
# Debian / Ubuntu
sudo apt install jq

# macOS
brew install jq

# Fedora / RHEL
sudo dnf install jq

# Arch
sudo pacman -S jq
```

## Installation

```bash
# Make executable and install to /usr/local/bin
chmod +x ipinfo
sudo cp ipinfo /usr/local/bin/
```

## How It Works

1. Accepts a single IP address as an argument.
2. Sends a request to `http://ipwho.is/<ip>`.
3. Validates the JSON response and checks for API-level errors.
4. Prints the full result with `jq` formatting.

## Error Handling

| Situation | Message |
|---|---|
| No argument provided | `Usage: ipinfo <ip>` |
| `jq` not installed | `Error: jq is not installed.` |
| Invalid JSON from API | `Error: Invalid JSON response` |
| API returns `success: false` | `Error: <api message>` |

## License

MIT — see [LICENSE](LICENSE) for details.
