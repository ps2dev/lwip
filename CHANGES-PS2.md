# Changes to lwIP for PS2

Last updated for lwIP 2.2.1.

## pbuf.c

`pbuf_alloc` no longer aligns the payload field for `PBUF_RAM` allocations.  
This is so that frames being output will not be unaligned.  

Note: this still does not solve all cases. For example, generating a UDP packet
will result in an unaligned final address, as `PBUF_TRANSPORT` is a general
"one size fits all" option.

Without this patch, the system will hang when making the initial connection.  

## tcp_out.c

Code that performs unaligned accesses now uses the added type `u32_opt_t`.

Without this patch, an address error exception will occur.  
