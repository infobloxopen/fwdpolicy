# fwdpolicy

## Name

*fwdpolicy* - is an alternate version of CoreDNS's *forward* plugin that adds the ability to define new
forwarding policies via plugins.

## Description

The *fwdpolicy* plugin is a copy of the *forward* plugin from https://github.com/coredns/coredns with an additional
feature that enables you to add new policies via external plugins.

## Syntax

Syntax is identical to the *forward* plugin from coredns/coredns. See `README-forward.md`, which
is a copy of the forward plugin README from coredns/coredns.

## Forwarding Policy Plugins

Below is a list of forwarding policy plugins that work with this plugin. If you develop a forwarding policy plugin 
and think it can be useful to others, please submit a PR to add it to this list.

[conditional](https://github.com/chrisohaver/conditional) - enables expression based forwarding policies

## Writing a Forwarding Policy Plugin

Any plugin that implements the `Policy` interface can be used as a forwarding policy plugin.

```golang
package fwdpolicy
type Policy interface {
	List(context.Context, []*Proxy, *request.Request) []*Proxy
	String() string
}
```

`List` should return an ordered list of Proxy (upstream servers) based on the desired policy behavior.
_fwdpolicy_, exactly as _forward_ plugin will attempt to forward to the returned proxy servers in order received,
stopping when successful or total time elapsed exceeds timeout.

`String` should return the string value used when selecting the policy in the Corefile.

## Examples

Forward to upstream servers `10.0.0.10`, `10.0.0.11`, and `10.0.0.12` using the forwarding policy defined in 
the _mypolicy_ plugin.

```
. {
  mypolicy
  fwdpolicy . 10.0.0.10 10.0.0.11 10.0.0.12 {
    policy mypolicy
  }
}

```
