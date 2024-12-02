# system-info-bash

# Output file
OUTPUT_FILE="/tmp/system_info.txt"

# Header
echo "System Information Report" > "$OUTPUT_FILE"
echo "Generated on: $(date)" >> "$OUTPUT_FILE"
echo "===================================" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# System Hostname
echo "Hostname: $(hostname)" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Operating System
echo "Operating System: $(lsb_release -d | cut -f2-)" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# System Uptime
echo "System Uptime: $(uptime -p)" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Linux Kernel Version
echo "Linux Kernel Version: $(uname -r)" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# CPU Information
echo "CPU Information:" >> "$OUTPUT_FILE"
lscpu | grep -E 'Model name|Architecture|CPU MHz' >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Memory Information
echo "Memory Information:" >> "$OUTPUT_FILE"
free -h >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# IP and MAC Address Information
echo "Network Interfaces:" >> "$OUTPUT_FILE"
ip -br address show | awk '{print $1, $3, $NF}' >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Filesystem Utilization
echo "Filesystem Utilization:" >> "$OUTPUT_FILE"
df -hT >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Last 5 'error' Lines from General Log
echo "Last 5 'error' Log Entries:" >> "$OUTPUT_FILE"
journalctl | grep -i "error" | tail -n 5 >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

# Completion Message
echo "System information has been written to $OUTPUT_FILE"
