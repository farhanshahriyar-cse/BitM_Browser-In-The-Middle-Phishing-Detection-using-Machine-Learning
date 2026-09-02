!apt-get install tshark

=============

#/content/victim bridge vnc.pcap
!gdown 1pTQry-oYDSPtXdw5jgGG-fzw8jPuWoDI

#/content/victim bridge normal.pcap
!gdown 11BDymdo1ezcJExZy3SNoU7arFMa_oXoR

!tshark -r '/content/victim bridge normal.pcap' -T fields -E header=y -E separator=, \
-E quote=d -E occurrence=f \
-e \_ws.expert.severity \
-e \_ws.expert.group \
\
-e frame.encap_type \
-e frame.time \
-e frame.offset_shift \
-e frame.time_epoch \
-e frame.time_delta \
-e frame.time_delta_displayed \
-e frame.time_relative \
-e frame.number \
-e frame.len \
-e frame.cap_len \
-e frame.marked \
-e frame.ignored \
-e frame.protocols \
-e frame.coloring_rule.name \
-e frame.coloring_rule.string \
-e sll.pkttype \
-e sll.hatype \
-e sll.halen \
-e sll.src.eth \
-e sll.unused \
-e sll.etype \
-e ip.version \
-e ip.hdr_len \
-e ip.dsfield \
-e ip.dsfield.dscp \
-e ip.dsfield.ecn \
-e ip.len \
-e ip.id \
-e ip.flags \
-e ip.flags.rb \
-e ip.flags.df \
-e ip.flags.mf \
-e ip.frag_offset \
-e ip.ttl \
-e ip.proto \
-e ip.checksum \
-e ip.checksum.status \
-e ip.src \
-e ip.dst \
-e tcp.srcport \
-e tcp.dstport \
-e tcp.stream \
-e tcp.completeness \
-e tcp.len \
-e tcp.seq \
-e tcp.seq_raw \
-e tcp.nxtseq \
-e tcp.ack \
-e tcp.ack_raw \
-e tcp.hdr_len \
-e tcp.flags \
\
-e tcp.flags.cwr \
\
-e tcp.flags.urg \
-e tcp.flags.ack \
-e tcp.flags.push \
-e tcp.flags.reset \
-e tcp.flags.syn \
-e tcp.flags.fin \
-e tcp.flags.str \
-e tcp.window_size_value \
-e tcp.window_size \
-e tcp.window_size_scalefactor \
-e tcp.checksum \
-e tcp.checksum.status \
-e tcp.urgent_pointer \
-e tcp.options \
-e tcp.options.nop \
-e tcp.option_kind \
-e tcp.options.nop \
-e tcp.option_kind \
-e tcp.options.timestamp \
-e tcp.option_kind \
-e tcp.option_len \
-e tcp.options.timestamp.tsval \
-e tcp.options.timestamp.tsecr \
-e tcp.time_relative \
-e tcp.time_delta \
-e tcp.analysis.bytes_in_flight \
-e tcp.analysis.push_bytes_sent \
-e tcp.payload \
-e data.len \
-e tls.record.opaque_type \
-e tls.record.version \
-e tls.record.length \
-e tls.app_data \
-e tls.app_data_proto \
-e tls.record.content_type \
-e tls.record.version \
-e tls.handshake.type \
-e tls.handshake.session_id_length \
-e tls.handshake.session_id \
-e tls.handshake.cipher_suites_length \
-e tls.handshake.extension.type \
-e udp.srcport \
-e udp.dstport \
-e udp.length \
-e udp.checksum \
-e udp.checksum.status \
-e udp.stream \
\
-e udp.time_relative \
-e udp.time_delta \
\
-e udp.payload \
-e dns.id \
-e dns.flags \
-e dns.flags.response \
-e dns.flags.opcode \
-e dns.flags.truncated \
-e dns.flags.recdesired \
-e dns.flags.z \
-e dns.flags.authenticated \
-e dns.flags.checkdisable \
\
-e dns.count.queries \
-e dns.count.answers \
-e dns.count.auth_rr \
-e dns.count.add_rr \
\
-e dns.qry.name \
-e dns.qry.name.len \
-e dns.count.labels \
-e dns.qry.type \
-e dns.qry.class \
\
-e dns.response_in \
-e dns.resp.name \
-e dns.resp.type \
-e dns.rr.udp_payload_size \
-e dns.resp.ext_rcode \
-e dns.resp.edns0_version \
-e dns.resp.z \
\
-e dns.resp.z.do \
-e dns.resp.z.reserved \
-e dns.resp.len \
-e dns.time \
\
-e quic.connection.number \
-e quic.packet_length \
-e quic.header_form \
-e quic.fixed_bit \
-e quic.spin_bit \
-e quic.dcid \
-e quic.remaining_payload > normal.csv

import pandas as pd

# Read the CSV file

csv_filename1 = 'normal.csv' # Replace with your CSV file's name
data_frame1 = pd.read_csv(csv_filename1)
