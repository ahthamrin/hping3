# hping3
Patch of hping3_3.a2.ds2-10 (Debian)

Allow signature with sequence number and rotate source port.
1. Signature must end with a contiguous underscores (_), example: abc___ will become `abc000` to `abc999` then it rotates back to `abc000`.
2. `-s <init_port>` option accepts `-s <init_port>-<last_port>` format. If defined, the source port increases up to `last_port` instead of 65535 then rotates.

## Example:
`hping3 -n -S -s 4000-4010 -p 3000 --udp -i 1 -e abcd____  10.10.10.10`

sends packets from this host to the destination 
1. src port 4000 with payload signature abcd0000,
2. src port 4001 payload abcd0001, ...
3. src port 4009 payload abcd0009,
4. src port 4000 payload abcd0010, ...

