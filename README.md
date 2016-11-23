## Table of Contents

1. [Overview](#overview)
1. [Usage - Most commonly used data type aliases](#usage)
1. [Reference - Full listing of data type aliases](#reference)

## Overview

This module provides some data types aliases (introduced in Puppet 4.4) for
working with IP addresses.

## Usage

This module provides some data types aliases which can be used to simplify type
checking in your Puppet 4.4+ compatible code. The most common aliases are
likely to be `IP::Address`, `IP::Address::V4`, and `IP::Address::V6`.

### `IP::Address`

The `IP::Address` alias will match any IP address, including both IPv4 and IPv6
addresses. It will match them either with or without an address prefix as used
in CIDR format IPv4 addresses.

#### Examples

~~~puppet
'127.0.0.1' =~ IP::Address                                # true
'8.8.4.4' =~ IP::Address                                  # true
'10.1.240.4/24' =~ IP::Address                            # true
'52.10.10.141' =~ IP::Address                             # true
'192.168.1' =~ IP::Address                                # false
'FEDC:BA98:7654:3210:FEDC:BA98:7654:3210' =~ IP::Address  # true
'FF01:0:0:0:0:0:0:101' =~ IP::Address                     # true
'FF01::101' =~ IP::Address                                # true
'FF01:0:0:0:0:0:0:101/32' =~ IP::Address                  # true
'FF01::101/60' =~ IP::Address                             # true
'::' =~ IP::Address                                       # true
'12AB::CD30:192.168.0.1' =~ IP::Address                   # true
'FE80::1%eth0' =~ IP::Address                             # true
~~~

### `IP::Address::V4`

The `IP::Address::V4` alias will match any string consisting of an IPv4 address
in the quad-dotted decimal format, with or without a CIDR prefix. It will not
match any abbreviated form (e.g., `192.168.1`) because these are poorly
documented and inconsistently supported.

#### Examples

~~~puppet
'127.0.0.1' =~ IP::Address::V4                                # true
'8.8.4.4' =~ IP::Address::V4                                  # true
'10.1.240.4/24' =~ IP::Address::V4                            # true
'52.10.10.141' =~ IP::Address::V4                             # true
'192.168.1' =~ IP::Address::V4                                # false
'FEDC:BA98:7654:3210:FEDC:BA98:7654:3210' =~ IP::Address::V4  # false
'12AB::CD30:192.168.0.1' =~ IP::Address::V4                   # false
~~~

### `IP::Address::V6`

The `IP::Address::V6` alias will match any string consistenting of an IPv6
address in any of the documented formats in RFC 2373, with or without an
address prefix.

#### Examples

~~~puppet
'127.0.0.1' =~ IP::Address::V6                                # false
'10.1.240.4/24' =~ IP::Address::V6                            # true
'FEDC:BA98:7654:3210:FEDC:BA98:7654:3210' =~ IP::Address::V6  # true
'FF01:0:0:0:0:0:0:101' =~ IP::Address::V6                     # true
'FF01::101' =~ IP::Address::V6                                # true
'FF01:0:0:0:0:0:0:101/32' =~ IP::Address::V6                  # true
'FF01::101/60' =~ IP::Address::V6                             # true
'::' =~ IP::Address::V6                                       # true
'12AB::CD30:192.168.0.1' =~ IP::Address::V6                   # true
'FE80::1%eth0' =~ IP::Address::V6                             # true
~~~

## Reference

### `IP::Address`

The `IP::Address` alias will match any IP address, including both IPv4 and IPv6
addresses. It will match them either with or without an address prefix as used
in CIDR format IPv4 addresses.

### `IP::Address::V4`

The `IP::Address::V4` alias will match any string consisting of an IPv4 address
in the quad-dotted decimal format, with or without a CIDR prefix. It will not
match any abbreviated form (e.g., `192.168.1`) because these are poorly
documented and inconsistently supported.

### `IP::Address::V6`

The `IP::Address::V6` alias will match any string consistenting of an IPv6
address in any of the documented formats in RFC 2373, with or without an
address prefix.

### `IP::Address::NoSubnet`

The `IP::Address::NoSubnet` alias will match the same things as the
`IP::Address` alias, except it will not match an address that includes an
address prefix (e.g., it will match `192.168.0.6` but not `192.168.0.6/24`).

### `IP::Address::V4::CIDR`

The `IP::Address::V4::CIDR` alias will match an IPv4 address in the CIDR
format. It will only match if the address contains an address prefix (e.g., it
will match `192.168.0.6/24` but not `192.168.0.6`).

### `IP::Address::V4::NoSubnet`

The `IP::Address::V4::NoSubnet` alias will match an IPv4 address only if the
address does not contain an address prefix (e.g., it will match `192.168.0.6`
but not `192.168.0.6/24`).

### `IP::Address::V6::Full`

The `IP::Address::V6::Full` alias will match an IPv6 address formatted in the
"preferred form" as documented in section 2.2.1 of RFC 2373, with or without an
address prefix as documented in section 2.3 of RFC 2373.

### `IP::Address::V6::Compressed`

The `IP::Address::V6::Compressed` alias will match an IPv6 address which may
contain `::` used to compress zeros as documented in section 2.2.2 of RFC 2373.
It will match addresses with or without an address prefix as documented in
section 2.3 of RFC 2373.
Additionally matched are link-local IPv6 addresses beginning with fe80: and
suffixed with %interface zone_id, as mentioned in section 11.2 of RFC 4007.

### `IP::Address::V6::Alternative`

The `IP::Address::V6::Alternative` alias will match an IPv6 address formatted
in the "alternative form" allowing for representing the last two 16-bit pieces
of the address with a quad-dotted decimal, as documented in section 2.2.1 of
RFC 2373. It will match addresses with or without an address prefix as
documented in section 2.3 of RFC 2373.

### `IP::Address::V6::NoSubnet::Full`

The `IP::Address::V6::NoSubnet::Full` alias will match an IPv6 address
formatted in the "preferred form" as documented in section 2.2.1 of RFC 2373.
It will not match addresses with address prefix as documented in section 2.3
of RFC 2373.

### `IP::Address::V6::NoSubnet::Compressed`

The `IP::Address::V6::NoSubnet::Compressed` alias will match an IPv6 address
which may contain `::` used to compress zeros as documented in section 2.2.2 of
RFC 2373. It will only match addresses without an address prefix as documented
in section 2.3 of RFC 2373.
Additionally matched are link-local IPv6 addresses beginning with fe80: and
suffixed with %interface zone_id, as mentioned in section 11.2 of RFC 4007.

### `IP::Address::V6::Alternative`

The `IP::Address::V6::Alternative` alias will match an IPv6 address formatted
in the "alternative form" allowing for representing the last two 16-bit pieces
of the address with a quad-dotted decimal, as documented in section 2.2.1 of
RFC 2373. It will only match addresses without an address prefix as documented
in section 2.3 of RFC 2373.
