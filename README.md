⚙️ Configuration
Before running a scan, configure your cloud provider credentials. V4Reclaim uses a .env file or environment variables.

Bash
v4reclaim configure
You will be prompted to enter your respective read-only access keys:

AWS_ACCESS_KEY_ID & AWS_SECRET_ACCESS_KEY

VERCEL_API_TOKEN (for edge environment scanning)

Note: For remediation (auto-release) features, ensure your IAM role has the necessary ec2:ReleaseAddress permissions.

💻 Usage
1. The Dry Run (Audit Only)
Run a sweeping audit across all configured environments. This will not modify or release any resources.

Bash
v4reclaim scan --provider aws --region all
Example Output:

Plaintext
[INFO] Scanning AWS environment (All Regions)...
[WARN] Found 3 unattached Elastic IPs in us-east-1.
       - 198.51.100.23 (Unattached for 45 days)
       - 198.51.100.89 (Unattached for 12 days)
       - 203.0.113.12  (Unattached for 120 days)
[WARN] Found 1 redundant NAT Gateway in eu-west-1.
--------------------------------------------------
💸 Estimated Monthly IPv4 Waste: $18.25
💡 Recommendation: Release unattached EIPs. Route eu-west-1 subnets through a shared NAT.
2. The Auto-Reclaim
Automatically release IPs that have been unattached for more than a specified number of days.

Bash
v4reclaim clean --max-idle-days 30 --auto-approve
3. Webhook / n8n Integration
Generate a JSON report and POST it to a custom webhook (ideal for triggering automated Slack alerts via n8n or Make).

Bash
v4reclaim scan --format json --webhook [https://your-n8n-instance.com/webhook/v4-alert](https://your-n8n-instance.com/webhook/v4-alert)
🏗️ Architecture & Stack
V4Reclaim is built with:

TypeScript / Node.js for fast, cross-platform CLI execution.

Commander.js for robust CLI interface parsing.

Boto3 / AWS SDK for direct infrastructure querying.

🤝 Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change. Ensure all tests pass before submitting.

Fork the Project

Create your Feature Branch (git checkout -b feature/AmazingFeature)

Commit your Changes (git commit -m 'Add some AmazingFeature')

Push to the Branch (git push origin feature/AmazingFeature)

Open a Pull Request

📄 License
Distributed under the MIT License. See LICENSE for more information.
"""

file_path = "/mnt/data/V4Reclaim_README.md"
with open(file_path, "w") as file:
file.write(readme_content)

print(f"File generated successfully at {file_path}")
