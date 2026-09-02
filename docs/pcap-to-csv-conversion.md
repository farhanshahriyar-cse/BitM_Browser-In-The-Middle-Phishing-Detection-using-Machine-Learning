# How to Convert a PCAP File to CSV Using Wireshark's TShark and Python

Converting a **PCAP (packet capture) file to CSV** is a common first step when preparing network traffic data for **machine learning**, **intrusion detection**, or **phishing/malware analysis** — such as building datasets for a Browser-in-the-Middle (BitM) attack detector. This guide walks through extracting packet-level fields from a `.pcap` file recorded in Wireshark, converting them into a clean CSV using **TShark** (Wireshark's command-line tool), and loading the result into a **Pandas DataFrame** in Python for further processing.

## Table of Contents

- [Why Convert PCAP to CSV?](#why-convert-pcap-to-csv)
- [Prerequisites](#prerequisites)
- [Step 1: Install TShark](#step-1-install-tshark)
- [Step 2: Download the PCAP Files](#step-2-download-the-pcap-files)
- [Step 3: Extract Packet Fields to CSV with TShark](#step-3-extract-packet-fields-to-csv-with-tshark)
- [Extracted Field Reference](#extracted-field-reference)
- [Step 4: Load the CSV into Pandas](#step-4-load-the-csv-into-pandas)
- [Troubleshooting](#troubleshooting)

## Why Convert PCAP to CSV?

Raw `.pcap` files captured by Wireshark or `tcpdump` aren't directly usable by most data science or machine learning tools. Converting network packets into a **structured CSV format** makes it possible to:

- Feed traffic data into pandas, scikit-learn, or deep learning pipelines
- Engineer features for **network intrusion detection systems (NIDS)**
- Build labeled datasets to detect **Browser-in-the-Middle (BitM)** or man-in-the-middle attacks
- Analyze TCP/IP, TLS, DNS, and QUIC traffic at scale using SQL or spreadsheet tools

## Prerequisites

- Wireshark / TShark installed (or a Colab/Linux environment where it can be installed via `apt-get`)
- Python 3 with `pandas` installed
- A `.pcap` or `.pcapng` capture file

## Step 1: Install TShark

TShark is the command-line counterpart to Wireshark and does the heavy lifting of parsing packets.

```bash
!apt-get install tshark
```

> The `!` prefix is only needed if you're running this in a Google Colab or Jupyter notebook. In a regular terminal, drop the `!`:
> `apt-get install tshark`

## Step 2: Download the PCAP Files

In this example, the capture files are hosted on Google Drive and pulled down with `gdown`:

```bash
# /content/victim bridge vnc.pcap
!gdown 1pTQry-oYDSPtXdw5jgGG-fzw8jPuWoDI

# /content/victim bridge normal.pcap
!gdown 11BDymdo1ezcJExZy3SNoU7arFMa_oXoR
```

Replace these with your own PCAP file paths if you're working with locally captured traffic.

## Step 3: Extract Packet Fields to CSV with TShark

This is the core step: TShark reads the `.pcap` file and exports the fields you specify into a CSV. The command below extracts a comprehensive set of fields covering Ethernet, IP, TCP, TLS, UDP, DNS, and QUIC layers — useful for building a rich network traffic dataset.

```bash
tshark -r "/content/victim bridge normal.pcap" \
  -T fields -E header=y -E separator=, -E quote=d -E occurrence=f \
  -e _ws.expert.severity -e _ws.expert.group \
  -e frame.encap_type -e frame.time -e frame.offset_shift -e frame.time_epoch \
  -e frame.time_delta -e frame.time_delta_displayed -e frame.time_relative \
  -e frame.number -e frame.len -e frame.cap_len -e frame.marked -e frame.ignored \
  -e frame.protocols -e frame.coloring_rule.name -e frame.coloring_rule.string \
  -e sll.pkttype -e sll.hatype -e sll.halen -e sll.src.eth -e sll.unused -e sll.etype \
  -e ip.version -e ip.hdr_len -e ip.dsfield -e ip.dsfield.dscp -e ip.dsfield.ecn \
  -e ip.len -e ip.id -e ip.flags -e ip.flags.rb -e ip.flags.df -e ip.flags.mf \
  -e ip.frag_offset -e ip.ttl -e ip.proto -e ip.checksum -e ip.checksum.status \
  -e ip.src -e ip.dst \
  -e tcp.srcport -e tcp.dstport -e tcp.stream -e tcp.completeness -e tcp.len \
  -e tcp.seq -e tcp.seq_raw -e tcp.nxtseq -e tcp.ack -e tcp.ack_raw -e tcp.hdr_len \
  -e tcp.flags -e tcp.flags.cwr -e tcp.flags.urg -e tcp.flags.ack -e tcp.flags.push \
  -e tcp.flags.reset -e tcp.flags.syn -e tcp.flags.fin -e tcp.flags.str \
  -e tcp.window_size_value -e tcp.window_size -e tcp.window_size_scalefactor \
  -e tcp.checksum -e tcp.checksum.status -e tcp.urgent_pointer -e tcp.options \
  -e tcp.options.nop -e tcp.option_kind -e tcp.options.timestamp -e tcp.option_len \
  -e tcp.options.timestamp.tsval -e tcp.options.timestamp.tsecr \
  -e tcp.time_relative -e tcp.time_delta -e tcp.analysis.bytes_in_flight \
  -e tcp.analysis.push_bytes_sent -e tcp.payload -e data.len \
  -e tls.record.opaque_type -e tls.record.version -e tls.record.length \
  -e tls.app_data -e tls.app_data_proto -e tls.record.content_type \
  -e tls.handshake.type -e tls.handshake.session_id_length -e tls.handshake.session_id \
  -e tls.handshake.cipher_suites_length -e tls.handshake.extension.type \
  -e udp.srcport -e udp.dstport -e udp.length -e udp.checksum -e udp.checksum.status \
  -e udp.stream -e udp.time_relative -e udp.time_delta -e udp.payload \
  -e dns.id -e dns.flags -e dns.flags.response -e dns.flags.opcode \
  -e dns.flags.truncated -e dns.flags.recdesired -e dns.flags.z \
  -e dns.flags.authenticated -e dns.flags.checkdisable \
  -e dns.count.queries -e dns.count.answers -e dns.count.auth_rr -e dns.count.add_rr \
  -e dns.qry.name -e dns.qry.name.len -e dns.count.labels -e dns.qry.type -e dns.qry.class \
  -e dns.response_in -e dns.resp.name -e dns.resp.type -e dns.rr.udp_payload_size \
  -e dns.resp.ext_rcode -e dns.resp.edns0_version -e dns.resp.z -e dns.resp.z.do \
  -e dns.resp.z.reserved -e dns.resp.len -e dns.time \
  -e quic.connection.number -e quic.packet_length -e quic.header_form \
  -e quic.fixed_bit -e quic.spin_bit -e quic.dcid -e quic.remaining_payload \
  > normal.csv
```

**Command flags explained:**

| Flag | Purpose |
|---|---|
| `-r <file>` | Input `.pcap`/`.pcapng` file to read |
| `-T fields` | Output only the specified fields (not the full packet dump) |
| `-E header=y` | Include a CSV header row with field names |
| `-E separator=,` | Use a comma as the field separator (CSV format) |
| `-E quote=d` | Wrap values in double quotes |
| `-E occurrence=f` | Output only the first occurrence of a repeated field |
| `-e <field>` | Field to extract (repeatable) |
| `> normal.csv` | Redirects output into a CSV file |

## Extracted Field Reference

The fields extracted above cover several protocol layers, useful for different analysis goals:

- **Frame metadata** — `frame.time`, `frame.len`, `frame.protocols`: timing and packet-size features
- **Ethernet/Linux cooked capture (SLL)** — `sll.*`: link-layer info
- **IP layer** — `ip.src`, `ip.dst`, `ip.ttl`, `ip.flags.*`: source/destination and routing behavior
- **TCP layer** — `tcp.flags.*`, `tcp.window_size`, `tcp.seq`: connection state and congestion behavior, key for detecting anomalous handshakes
- **TLS layer** — `tls.handshake.type`, `tls.record.content_type`: useful for spotting suspicious TLS/HTTPS handshakes (relevant to BitM/MITM detection)
- **UDP layer** — `udp.srcport`, `udp.dstport`, `udp.payload`
- **DNS layer** — `dns.qry.name`, `dns.flags.*`: domain lookups, useful for phishing-domain detection
- **QUIC layer** — `quic.*`: modern HTTP/3 transport fields

## Step 4: Load the CSV into Pandas

Once the CSV is generated, load it into a Pandas DataFrame for analysis, feature engineering, or feeding into a machine learning model:

```python
import pandas as pd

# Read the CSV file
csv_filename1 = "normal.csv"  # Replace with your CSV file's name
data_frame1 = pd.read_csv(csv_filename1)

# Quick sanity check
print(data_frame1.shape)
data_frame1.head()
```

Repeat Steps 3–4 for each additional `.pcap` file (e.g. the "victim bridge vnc.pcap" capture) to build out a full labeled dataset.

## Troubleshooting

- **`tshark: command not found`** — Make sure Wireshark/TShark is installed and on your system `PATH`.
- **Empty or missing fields in the CSV** — Not every packet contains every field (e.g. DNS fields only appear on DNS packets); empty cells are expected and normal.
- **File path errors on Windows** — Wrap paths containing spaces in double quotes, e.g. `-r "C:\captures\my file.pcap"`.
- **Large CSV files** — For big captures, consider using `-Y "<display filter>"` with TShark to pre-filter packets (e.g. only TCP or only DNS traffic) before exporting, reducing file size and pandas load time.

---

**Keywords:** pcap to csv, wireshark to csv, tshark tutorial, convert pcap file, network traffic csv, tshark command line, pandas network analysis, packet capture dataset, python network traffic analysis, phishing detection dataset, BitM attack detection
