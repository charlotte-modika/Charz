import socket

print("=== Simple Port Scanner ===")

target = input("Enter target IP or website: ")

try:
    target_ip = socket.gethostbyname(target)

    print(f"\nScanning {target_ip}...\n")

    common_ports = {
        21: "FTP",
        22: "SSH",
        23: "Telnet",
        25: "SMTP",
        53: "DNS",
        80: "HTTP",
        110: "POP3",
        143: "IMAP",
        443: "HTTPS",
        3306: "MySQL"
    }

    for port in common_ports:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)

        result = sock.connect_ex((target_ip, port))

        if result == 0:
            print(f"[OPEN] Port {port} - {common_ports[port]}")

        sock.close()

except socket.gaierror:
    print("Hostname could not be resolved.")

except KeyboardInterrupt:
    print("\nScan stopped.")
