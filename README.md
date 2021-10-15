# fwdpolicy

## Name

*fwdpolicy* - is an alternate version of CoreDNS's *forward* plugin that adds the ability to define new
forwarding policies via plugins.

## Description

The *fwdpolicy* plugin is a copy of the *forward* plugin from coredns/coredns with an additional
feature to add new policies via external plugin.

## Syntax

Syntax is identical to the *forward* plugin from coredns/coredns. See `README-forward.md`, which
is a copy of the forward plugin README from coredns/coredns.

## Writing a forwarding policy plugin

TODO

## Examples

Forward to upstream servers `10.0.0.10`, `10.0.0.11`, and `10.0.0.12` using the forwarding policy defined in 
the _mypolicy_ plugin.

```
. {
  mypolicy
  forward . 10.0.0.10 10.0.0.11 10.0.0.12 {
    policy mypolicy
  }
}

```