#!/usr/bin/make -f

# Portions of this file contributed by NIST are governed by the
# following statement:
#
# This software was developed at the National Institute of Standards
# and Technology by employees of the Federal Government in the course
# of their official duties. Pursuant to title 17 Section 105 of the
# United States Code this software is not subject to copyright
# protection and is in the public domain. NIST assumes no
# responsibility whatsoever for its use by other parties, and makes
# no guarantees, expressed or implied, about its quality,
# reliability, or any other characteristic.
#
# We would appreciate acknowledgement if the software is used.

SHELL := /bin/bash

PYTHON3 ?= python3

uco_srcdir := UCO

all: \
  $(uco_srcdir)/tests/uco_monolithic.ttl

# TODO: The check-supply-chain recipes should be written to descend into
# each submodule tracking a CDO (/UCO, etc.) repository and run its
# supply chain rule.  This recursive check is expected to be called most
# typically by the top_srcdir recipe check-supply-chain-dependencies.
.PHONY: \
  check-supply-chain \
  check-supply-chain-CDO-Shapes-Example

$(uco_srcdir)/.venv.done.log:
	$(MAKE) \
	  PYTHON3=$(PYTHON3) \
	  --directory $(uco_srcdir) \
	  .venv.done.log

$(uco_srcdir)/tests/uco_monolithic.ttl: \
  $(uco_srcdir)/.venv.done.log \
  $(uco_srcdir)/ontology/uco/master/uco.ttl
	$(MAKE) \
	  --directory $(uco_srcdir)/tests \
	  uco_monolithic.ttl

check: \
  all

check-supply-chain: \
  check-supply-chain-CDO-Shapes-Example

check-supply-chain-CDO-Shapes-Example:
	$(MAKE) \
	  --directory CDO-Shapes-Example \
	  check-supply-chain-dependencies
	$(MAKE) \
	  --directory CDO-Shapes-Example \
	  check-supply-chain

clean:
