# PoSh-oVirt

A PowerShell Module for OLVM (oVirt) Management.

Quick Intro:
All Functions and classes are prefaced with the lowercase letter "o" (for oVirt) to avoid PowerShell naming conflicts with other modules

Uses a "Connection Management" PSObject To store connection data required to maintain connectivity to each oVirt server

oVirt has what I term Base (or primary) objects and Secondary objects that are "children" of the Base objects, therefore
the secondary functions require the instantiation of base objects as a reference. I.e. an oVmNic can't exist without a base oVM

Base Objects can be displayed (after connecting to an oVirt Server) using the command:
Get-oVirt -oVirtServerName $oVirtServerName | Select -ExpandProperty Link | Sort "rel"

Note: most returned PSObjects have methods in their classes allowing users to retrieve additional properties about the object, not natively 
returned by oVirt. This also saves time by not retrieving data until/if needed for additional activity. Many of these additional properties 
are recursive, for additional drill down.

Note: This project is a work in progress, some of the functions were built based on (often vague) documentation, and I don't have a test 
environment with some of the features required to validate them. So if something doesn't work there is a framework for most of the objects, 
and a small handful of more obscure items, that I have not created yet. However following the format I've laid out, it should be possible to 
build or fix functions.

Note: This module can make use of several 3rd party software features if already installed by the user. Putty, Plink, Virtual Machine Manager, and Posh-SSH.
None are required, and are NOT INCLUDED with this sample code.

## Installation

Copy the Folder PoSh-oVirt to a valid PowerShell Modules path on your system. Typically found by opening a PowerShell console and typing:
$Env:PSModulePath -Split ';'

## Documentation

All User Functions have PowerShell Get-Help based documentation.
  Example:
  Get-Help Get-oVirt

## Examples

I use the following example to connect:

Get-Module -Name "Posh-oVirt" -ListAvailable | Import-Module
$oVirtServerName = "ServerName.Domain.com"
$oVirtCredential = (Get-Credential -UserName 'admin@internal' -Message "Enter Password for $($oVirtServerName)")
Connect-oVirtServer -oVirtServerName $oVirtServerName -oVirtCredential $oVirtCredential
Get-oVirt -oVirtServerName $oVirtServerName | Select *

## Security

Please consult the [security guide](./SECURITY.md) for our responsible security vulnerability disclosure process

## License

Copyright (c) 2024,2025 Oracle and/or its affiliates.

Released under the Universal Permissive License v1.0 as shown at
<https://oss.oracle.com/licenses/upl/>.
