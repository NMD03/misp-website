---
title: MISP 2.4.130 released (Various fixes, performance improvements and new features)
date: 2020-08-21
layout: post
banner: /img/blog/d4_sshd_widget.png
---

# MISP 2.4.130 released

A new version of MISP ([2.4.130](https://github.com/MISP/MISP/tree/v2.4.130)) has been released with performance improvements, multiple bugs fixed and new features.

# Speed improvements

- [internal] cache tags instead of loading them over and over via the
  event fetcher, fixes #6201.
  - should speed things up for exports of datasets that have a lot of recurring tags
  - moved the caching of some internals to the appmodel level to make it more generic
- [internal] Update correlations in one query.
  Before, for every event saving action, four queries for updating correlations were generated
- [correlations] Faster loading related attributes.
- [sync] drop the republishing of events when the modification is merely
  a timestamp bump.
  - due to an already fixed issue still lingering, invalid event edits keep getting synchronised between instances
  - these events still generate publish alerts erroneously
  - this fix compares the previous state of the event to the modification, if there are no material changes (attributes, objects, object relations, event tags added/updated) then the publishing is dropped.

# API improvements

- Allow tag deletion for an event on update
- Allow for attribute tag deletion via Event or Attribute edit. Clean and return the attribute tags on response from editing an attribute, update code to remove legacy
- [opendata export] Parsing portal url parameter + slight parameters
  parsing changes.
  - As the possibility of specifying the url of the
    Open data portal to use instead of the default
    one, we support here this parameter and adapt
    the way we build the command that will launch
    the python script
  - Slight changes to replace some isset tests by
    empty tests to make sure the concerned fields
    are not only set, but also contain a value

# Improvements

- [UI] Show event preview when merging.
- [attribute] Add support for IDN domains.
- New: [freetext] Convert `[at]` to `@` and `hxtp` and `htxp` to `http`
- [widgets] Additional widgets for sharing statistics and layouts.
- [CLI] Allow to fetch remove event by UUID.
- [stix import] Fixed port in ip-port objects import to lose src and dst
  context.
- [stix export] Fixed the slight difference between parsing x509
  fingerprint attributes and x509 objects.
- [stix export] Fixed x509 fingerprint attributes export & moved mapping
  dictionaries to the mapping script
  - Only the x509-fingerprint-sha1 attribute was
    exported, and as a standard sha1 attribute,
    which was a loss of context, now the x509
    fingerprint attributes (md5, sha1 & sha256) are
    exported as expected within a x509 observable
  - Also moved the mapping dictionaries with the
    appropriate indent to the mapping script, where
    they should belong

# Many bugs fixed and small improvements

Many other improvements are documented in the [complete changelog is available](/Changelog.txt).

# Acknowledgement

We would like to thank all the [contributors](/contributors), reporters and users who have helped us in the past months to improve MISP and information sharing at large. This release includes multiple updates in [misp-objects](/objects.html), [misp-taxonomies](/taxonomies.html) and [misp-galaxy](/galaxy.html).

As always, a detailed and [complete changelog is available](/Changelog.txt) with all the fixes, changes and improvements.


