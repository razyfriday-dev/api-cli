# Getting Started with Hostinger API CLI

Welcome to the Hostinger API Command Line Interface (`hapi`)! This guide will help you get up and running quickly.

## Prerequisites

- A Hostinger account with API access
- A valid API token from your Hostinger account
- Operating system: Linux, macOS, or Windows (with WSL)

## Installation

### Step 1: Download the Binary

Visit the [releases page](https://github.com/razyfriday-dev/api-cli/releases) and download the latest binary for your operating system.

#### Linux Installation

```bash
# Download the binary
wget https://github.com/razyfriday-dev/api-cli/releases/download/v1.0.0/hapi-v1.0.0-linux-amd64.tar.gz

# Extract the archive
tar xzf hapi-v1.0.0-linux-amd64.tar.gz

# Move to system path
sudo mv hapi /usr/local/bin/

# Verify installation
hapi --version
```

#### macOS Installation

```bash
# Download the binary
wget https://github.com/razyfriday-dev/api-cli/releases/download/v1.0.0/hapi-v1.0.0-darwin-amd64.tar.gz

# Extract the archive
tar xzf hapi-v1.0.0-darwin-amd64.tar.gz

# Move to system path
sudo mv hapi /usr/local/bin/

# Verify installation
hapi --version
```

#### Windows Installation

1. Download `hapi-v1.0.0-windows-amd64.zip` from the releases page
2. Extract the ZIP file to a folder (e.g., `C:\Program Files\hapi`)
3. Add the folder to your system PATH environment variable
4. Open PowerShell and verify: `hapi --version`

## Step 2: Obtain Your API Token

1. Log in to your [Hostinger account](https://hpanel.hostinger.com)
2. Navigate to **Settings** → **API Management** (or similar)
3. Click **Generate New Token**
4. Copy the token (you'll only see it once!)
5. Store it securely

## Step 3: Configure the CLI

Choose one of the configuration methods below:

### Option A: Configuration File (Recommended)

Create `~/.hapi.yaml`:

```bash
cat > ~/.hapi.yaml << 'EOF'
api_token: your_api_token_here
output_format: table
EOF
```

Set secure permissions:

```bash
chmod 600 ~/.hapi.yaml
```

### Option B: Environment Variable

```bash
export HAPI_API_TOKEN=your_api_token_here
```

### Option C: Command-Line Flag

```bash
hapi --config /path/to/config.yaml vps vm list
```

## Step 4: Verify Configuration

Test your setup:

```bash
hapi vps vm list
```

If successful, you'll see a list of your VPS instances.

## Common Commands

### List Your VPS Instances

```bash
hapi vps vm list
```

### Get Details About a Specific VPS

```bash
hapi vps vm get <instance-id>
```

### View Available Data Centers

```bash
hapi vps data-centers list
```

### Manage Firewall Rules

```bash
# List firewall rules
hapi vps firewall rules list <instance-id>

# Create a new rule
hapi vps firewall rules create <instance-id> \
  --action allow \
  --protocol tcp \
  --port 80
```

### Check VPS Metrics

```bash
hapi vps vm metrics <instance-id>
```

### Manage SSH Public Keys

```bash
# List public keys
hapi vps public-keys list

# Create a new public key
hapi vps public-keys create --name "my-key" --key "ssh-rsa AAAA..."

# Attach to VPS
hapi vps public-keys attach <key-id> <instance-id>
```

## Enable Shell Auto-Completion

Auto-completion makes the CLI easier to use. See [AUTOCOMPLETE.md](AUTOCOMPLETE.md) for detailed instructions.

### Quick Start (Bash)

```bash
hapi completion bash | sudo tee /etc/bash_completion.d/hapi
```

Then reload your shell:

```bash
exec bash
```

## Output Formats

The CLI supports multiple output formats. Set your preference in the config file or use the `--format` flag:

### Table Format (Default)

```bash
hapi vps vm list
```

### JSON Format

```bash
hapi vps vm list --format json
```

### Tree Format

```bash
hapi vps vm list --format tree
```

## Troubleshooting

### "Command not found: hapi"

- Verify the binary is in your PATH: `echo $PATH`
- Try the full path: `/usr/local/bin/hapi --version`
- If installed locally, use: `./hapi --version`

### "Invalid API token"

- Double-check your token in the configuration file
- Verify the token hasn't expired
- Generate a new token from your Hostinger account

### "Permission denied" Error

- Check file permissions: `ls -la ~/.hapi.yaml`
- Ensure the binary is executable: `chmod +x /usr/local/bin/hapi`

### "Connection timeout"

- Verify your internet connection
- Check if the Hostinger API is accessible: `ping api.hostinger.com`
- Try increasing the timeout in your config file

## Next Steps

1. **Explore the Full Command Reference**: See [CLI Reference](hapi.md)
2. **Learn Configuration Options**: Check [CONFIGURATION.md](CONFIGURATION.md)
3. **Enable Auto-Completion**: Follow [AUTOCOMPLETE.md](AUTOCOMPLETE.md)
4. **Read the API Documentation**: Visit [Hostinger Developer Docs](https://developers.hostinger.com)

## Getting Help

### View Help for Any Command

```bash
# General help
hapi --help

# VPS command help
hapi vps --help

# Specific command help
hapi vps vm list --help
```

### Report Issues

Found a bug? Please report it on [GitHub Issues](https://github.com/razyfriday-dev/api-cli/issues).

## Support

For API-related questions, visit the [Hostinger Developer Documentation](https://developers.hostinger.com).

## Additional Resources

- [Configuration Guide](CONFIGURATION.md)
- [Shell Auto-Completion Guide](AUTOCOMPLETE.md)
- [Full CLI Reference](hapi.md)
- [Hostinger API Documentation](https://developers.hostinger.com)

---

**Ready to get started?** Run your first command:

```bash
hapi vps vm list
```

Happy managing! 🚀
