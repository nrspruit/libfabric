---
layout: page
title: fi_rxm(7)
tagline: Libfabric Programmer's Manual
---
{% include JB/setup %}

# NAME

The RxM (RDM over MSG) Utility Provider

# OVERVIEW

The RxM provider (ofi_rxm) is an utility provider that supports RDM
endpoint emulated over MSG endpoint of a core provider.

# REQUIREMENTS

RxM provider requires the core provider to support the following features:

  * MSG endpoints (FI_EP_MSG)

  * RMA read/write (FI_RMA)

  * FI_OPT_CM_DATA_SIZE of atleast 24 bytes

# SUPPORTED FEATURES

The RxM provider currently supports *FI_MSG*, *FI_TAGGED* and *FI_RMA* capabilities.

*Endpoint types*
: The provider supports only *FI_EP_RDM*.

*Endpoint capabilities*
: The following data transfer interface is supported: *FI_MSG*, *FI_TAGGED*, *FI_RMA*.

*Progress*
: The RxM provider supports only *FI_PROGRESS_MANUAL* for now.

*Addressing Formats*
: FI_SOCKADDR, FI_SOCKADDR_IN

*Memory Region*
: FI_MR_VIRT_ADDR, FI_MR_ALLOCATED, FI_MR_PROV_KEY MR mode bits would be
  required from the app in case the core provider requires it.

# LIMITATIONS

When using RxM provider, some limitations from the underlying MSG provider could also show
up. Please refer to the corresponding MSG provider man pages to find about those limitations.

## Unsupported features

RxM provider does not support the following features:

  * op_flags: FI_CLAIM, FI_PEEK, FI_FENCE.

  * FI_ATOMIC

  * Scalable endpoints

  * Shared contexts

  * FABRIC_DIRECT

  * Multi recv

  * Counters

  * FI_MR_SCALABLE

  * Authorization keys

  * Application error data buffers

  * Multicast

  * FI_ADDR_STR, FI_SYNC_ERR

  * Reporting unknown source addr data as part of completions

  * Triggered operations

  * fi_cq_sread, fi_cq_sreadfrom and fi_cq_signal calls.

## Auto progress

When sending large messages, an app doing an sread or waiting on the CQ file descriptor
may not get a completion when reading the CQ after being woken up from the wait.
The app has to do sread or wait on the file descriptor again.

## Usage limitations

RxM provider should work fine for client - server programs like fabtests. Support for MPI, SHMEM
and other applications is work in progress.

# RUNTIME PARAMETERS

No runtime parameters are currently defined.

# SEE ALSO

[`fabric`(7)](fabric.7.html),
[`fi_provider`(7)](fi_provider.7.html),
[`fi_getinfo`(3)](fi_getinfo.3.html)
