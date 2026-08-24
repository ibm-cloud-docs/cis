---

copyright:
  years: 2018, 2026
lastupdated: "2026-08-24"

keywords: Helpful tools, whois, IPv4, HAR

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Helpful tools for managing your CIS deployment
{: #helpful-tools-for-managing-your-cis-deployment}

Some public-domain Unix system administration tools can help you manage your {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) deployment.
{: shortdesc}

## Sysadmin tools
{: #cis-sysadmin-tools}

* `whois` (domain identification tool)
* `dig` (DNS tool)
* `cURL` (HTTP and HTTPS tool)
* `netcat` (IP and port tool)
* `traceroute` (network tool)

## Commercial tools for external and remote testing
{: #commercial-tools-for-external-and-remote-testing}

* GTMetrix (HTTP)
* Web page test (HTTP)
* WhatsMyDNS (DNS tool)
* G Suite Toolbox (DNS and HTTP)

## Tools for looking at logs and history
{: #tools-for-looking-at-logs-and-history}

HTTP Archive files (HAR files)

### Using `whois`
{: #using-whois}

`whois` is a UNIX system command line tool that you can use to look up registrar information for a given domain name or IP address. For example, the domain’s given authoritative servers or the owner of a particular IP address.

Examples:

`whois example.com`

`whois 8.8.8.8`

### Using `dig`
{: #using-dig}

`dig` is a Unix command line tool that can perform DNS queries and check DNS records for a specific domain. It is similar to `nslookup`.

The schema of this command is `dig <record_type> <domainname> <options>`

For example:

- `dig example.com`
- `dig my.example.com`
- `dig example.com +trace`
- `dig NS example.com`
- `dig example.com @ns.example.com`

### Using `cURL`
{: #use-curl}

`cURL` is a Unix command line tool that lets you transmit data by using the URL syntax. It’s commonly used to make HTTP requests or compare server responses.

The schema for this command is: `curl -option1 -option2 http://example.com/url`

For example:

- `curl -svo /dev/null http://www.example.com`
- `curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`
- `curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`
- `curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Using `mtr` and `traceroute`
{: #using-mtr-and-traceroute}

`mtr` and `traceroute` are Unix command line tools that let you measure performance or latency along a specific network path to a specified host or destination server.

For example:

- `mtr -rwc 20 example.com -T -4`
- `mtr -rwc 20 8.8.8.8 -T -6`
- `traceroute example.com -T -4`
- `traceroute 8.8.8.8 -T -6`

| Option | Definition |
|---------|-----------|
| -c | Sets the number of pings sent |
| -T | Forces a TCP traceroute (normally ICMP) |
| -4 | Forces the use of IPv4 |
| -6 | Forces the use of IPv6 |
{: caption="Command options" caption-side="bottom"}

### Generating an HAR file
{: #generating-a-har-file}

An HAR file is a recording of HTTP requests from a web browser. Browsers, such as Chrome, have a Developer Tools section that can help you get set up to make HAR files. For more information on how to create a HAR file, see [How do I generate a HAR file?](/docs/cis?topic=cis-generate-har-files) in the troubleshooting section.

## Looking at logs and history by using My Traceroute
{: #mtr-overview}

MTR (My Traceroute) is a network diagnostic tool that combines the functions of traceroute and ping into a single program. Where traceroute shows the path that packets take to reach a destination, and ping measures round-trip time to a single host, MTR does both simultaneously and continuously. MTR probes each hop on the network path repeatedly, collecting statistics such as packet loss percentage, average latency, and jitter for every intermediate router between your source and destination.

MTR is valuable for diagnosing intermittent network issues that a one-time traceroute might miss. By running continuously over time, MTR reveals unstable hops, asymmetric packet loss, and routing anomalies that are otherwise difficult to detect.

### MTR output fields
{: #mtr-output-fields}

The following table describes the columns in MTR output.

| Field |	Description |
| ------- | ---------- |
| Host |	The hostname or IP address of the hop. |
| Loss% |	The percentage of packets lost at this hop. |
| Snt |	The total number of packets sent to this hop. |
| Last |	The round-trip time (in milliseconds) of the most recent packet. |
| Avg	| The average round-trip time across all packets sent. |
| Best |	The best (lowest) round-trip time recorded. |
| Wrst |	The worst (highest) round-trip time recorded. |
| StDev |	The standard deviation of round-trip times, indicating jitter. |
{: caption="MTR output fields" caption-side="bottom"}

Packet loss that is shown at an intermediate hop does not always indicate a problem at that hop. Many routers deprioritize or rate-limit ICMP traffic that is used by MTR while still forwarding data traffic normally. Investigate a hop as a potential problem only if loss persists at that hop and all subsequent hops.
{: important}

### Generating an MTR report on Linux
{: #mtr-linux}

MTR is available on most Linux distributions and can be installed from the default package manager.

#### Prerequisites
{: #mtr-linux-prereqs}

* Root or sudo access on the Linux host.
* MTR installed. If MTR is not installed, install it using the package manager for your distribution:
   * RHEL or CentOS or Fedora:
     ```sh
     sudo yum install mtr
     ```
     {: pre}

   * Debian or Ubuntu:
     ```sh
     sudo apt-get install mtr
     ```
     {: pre}

#### Running MTR and traceroute
{: #mtr-traceroute}

You can use either MTR or traceroute to identify the network path between your system and a destination. While traceroute performs a one-time trace of the route, MTR continuously probes each network hop and collects latency and packet loss statistics. MTR is recommended when you are troubleshooting intermittent connectivity or performance issues because it provides more comprehensive diagnostic information.

The following examples show how to run MTR and traceroute using TCP probes over IPv4 and IPv6.

- `mtr -rwc 20 example.com -T -4`
- `mtr -rwc 20 8.8.8.8 -T -6`
- `traceroute example.com -T -4`
- `traceroute 8.8.8.8 -T -6`

| Option | Definition |
|---------|-----------|
| -c | Sets the number of pings sent |
| -T | Forces a TCP traceroute (normally ICMP) |
| -4 | Forces the use of IPv4 |
| -6 | Forces the use of IPv6 |
{: caption="Command options" caption-side="bottom"}

### Running MTR in report mode
{: #mtr-linux-run}

Use report mode (`--report`) to collect a fixed number of samples and print a summary. This is the recommended format for sharing MTR results with support teams.

```sh
mtr --report --report-cycles 60 <destination>
```
{: pre}

Replace `<destination>` with the hostname or IP address that you want to trace. For example, to diagnose connectivity to a CIS-proxied domain:

```sh
mtr --report --report-cycles 60 example.com
```
{: pre}

The `--report-cycles 60` flag sends 60 packets to each hop before you print the report. Increasing the cycle count provides more statistically reliable results for intermittent issues.

### Saving MTR output to a file
{: #mtr-linux-save}

To save the report to a file for sharing with support:

```sh
mtr --report --report-cycles 60 example.com > mtr-report.txt
```
{: pre}

### Generating an MTR report on Windows (WinMTR)
{: #mtr-windows}

WinMTR is the Windows equivalent of the MTR tool. It provides a graphical user interface (GUI) and can also export results as text or HTML files.

#### Prerequisites
{: #mtr-windows-prereqs}

- Administrator rights are recommended for accurate results.
- WinMTR downloaded from the [WinMTR project page](https://sourceforge.net/projects/winmtr/){: external}.

#### Running WinMTR
{: #mtr-windows-run}

1. Extract the WinMTR compressed file archive and run `WinMTR.exe`. No installation is required.
2. In the **Host** field, enter the hostname or IP address of your destination. For example, enter `example.com` to trace the path to a CIS-proxied domain.
3. Click **Start** to begin collecting data. Allow WinMTR to run for at least **5 minutes** (or longer for intermittent issues) to accumulate enough samples for meaningful statistics.
4. Click **Stop** when you collect sufficient data.

#### Exporting WinMTR results
{: #mtr-windows-export}

WinMTR can export results in two formats:

* **Export TEXT**: Saves a plain-text summary that is suitable for pasting into a support ticket.
* **Export HTML**: Saves an HTML file with the full hop-by-hop table.

To export your results, click **Export TEXT** or **Export HTML** in the WinMTR toolbar, then choose a save location.

### WinMTR output fields
{: #mtr-windows-output-fields}

WinMTR displays the same diagnostic statistics as the Linux MTR tool. For field descriptions, see [MTR output fields](#mtr-output-fields).

When you open a support case with IBM Cloud CIS, always include both a forward MTR (from your host to the CIS endpoint) and a reverse MTR (from a host near the CIS endpoint back to your IP, if possible). Asymmetric routing means that the outbound and return paths can differ, and both reports help support teams pinpoint the problem.
{: tip}


## Interpreting MTR results with CIS
{: #mtr-cis-interpret}

When you experience connectivity issues with your CIS-proxied domain, use the following guidelines to interpret your MTR output:

* **Loss only at one intermediate hop, not at subsequent hops**: The router at that hop rate-limits ICMP. This is not a network problem.
* **Loss starting at a specific hop and continuing through all subsequent hops**: The problem is at or before that hop. Share the MTR report with IBM Cloud Support.
* **High latency at the first hop**: Check your local network and default gateway.
* **High latency at a CIS anycast IP hop**: Open an IBM Cloud Support case and include your MTR report. You can identify CIS anycast IPs by looking for Cloudflare or IBM Cloud network ASN entries in the hop list.
