# Configuration Guide

The Hostinger API CLI (`hapi`) can be configured in multiple ways. This guide explains all configuration options and methods.

## Configuration Methods

The CLI supports three configuration methods (in order of precedence):

1. **Command-line flags** - Highest priority
2. **Environment variables** - Medium priority  
3. **Configuration file** - Lowest priority

## Configuration File

By default, the CLI reads configuration from `$HOME/.hapi.yaml`.

### Specifying a Custom Configuration File

Use the `--config` flag to specify a custom configuration file location:

```bash
hapi --config /path/to/custom-config.yaml vps vm list
```

### Configuration File Format

The configuration file is in YAML format. Here's a complete example:

```yaml
# API Authentication
api_token: your_api_token_here

# API Endpoint (optional)
api_url: https://api.hostinger.com

# Default output format (json|table|tree)
output_format: table

# Request timeout in seconds (optional)
request_timeout: 30

# Enable verbose logging (optional)
verbose: false

# Debug mode (optional)
debug: false
```

## Environment Variables

All configuration file properties can be set via environment variables with the `HAPI_` prefix in UPPERCASE.

### Available Environment Variables

| Configuration Key | Environment Variable | Type | Description |
|---|---|---|---|
| `api_token` | `HAPI_API_TOKEN` | string | Your Hostinger API token (required) |
| `api_url` | `HAPI_API_URL` | string | Hostinger API endpoint (optional) |
| `output_format` | `HAPI_OUTPUT_FORMAT` | string | Default output format: json, table, or tree |
| `request_timeout` | `HAPI_REQUEST_TIMEOUT` | integer | Request timeout in seconds |
| `verbose` | `HAPI_VERBOSE` | boolean | Enable verbose output |
| `debug` | `HAPI_DEBUG` | boolean | Enable debug mode |

### Example: Using Environment Variables

```bash
export HAPI_API_TOKEN=your_api_token_here
export HAPI_OUTPUT_FORMAT=json
hapi vps vm list
```

## Command-Line Flags

Use flags to override configuration file and environment variable settings.

### Global Flags

```bash
hapi --config <file>      # Specify configuration file location
hapi --format <format>    # Set output format (json|table|tree)
hapi -h, --help          # Show help information
```

### Example: Using Flags

```bash
# Use JSON output format
hapi --format json vps vm list

# Use custom config file and JSON output
hapi --config ~/custom-config.yaml --format json vps vm list
```

## Configuration Priority Example

```bash
# Configuration file: /etc/hapi/config.yaml
# - output_format: table
# - api_token: from_config_file

# Environment variable:
# - HAPI_OUTPUT_FORMAT=json

# Command:
hapi --format tree vps vm list

# Result: tree format is used (highest priority)
```

## Output Formats

The CLI supports three output formats:

### Table Format (Default)
```
ID      NAME           STATUS    RAM    CPU
-----   -----------    ------    ---    ---
12345   my-server      active    4GB    2
```

### JSON Format
```json
{
  "id": 12345,
  "name": "my-server",
  "status": "active",
  "ram": "4GB",
  "cpu": 2
}
```

### Tree Format
```
my-server (ID: 12345)
├── status: active
├── ram: 4GB
└── cpu: 2
```

## Best Practices

1. **Security**: Store API tokens securely
   - Never commit `hapi.yaml` to version control
   - Use environment variables in CI/CD pipelines
   - Restrict file permissions: `chmod 600 ~/.hapi.yaml`

2. **Organization**: Use separate config files for different environments
   ```bash
   hapi --config ~/.hapi.production.yaml ...
   hapi --config ~/.hapi.staging.yaml ...
   ```

3. **Default Format**: Set your preferred output format in the config file
   ```yaml
   output_format: json
   ```

4. **Documentation**: Document your configuration approach for your team

## Getting Your API Token

To obtain your API token:

1. Log in to your Hostinger account
2. Navigate to API Management
3. Generate a new API token
4. Copy and store it securely

## Troubleshooting

### "Config file not found" Error
- Ensure the config file path is correct
- Check file permissions: `ls -la ~/.hapi.yaml`
- Verify the file is in YAML format

### "Invalid API token" Error
- Verify the API token is correct in your configuration
- Check that the token has not expired
- Generate a new token if necessary

### "Timeout" Error
- Increase `request_timeout` in configuration
- Check your network connectivity
- Verify the API endpoint is accessible

## See Also

- [Getting Started Guide](GETTING_STARTED.md)
- [CLI Reference](hapi.md)
- [Hostinger API Documentation](https://developers.hostinger.com)
