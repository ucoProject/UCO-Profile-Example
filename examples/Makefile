#!/usr/bin/make -f

# Portions of this file contributed by NIST are governed by the
# following statement:
#
# This software was developed at the National Institute of Standards
# and Technology by employees of the Federal Government in the course
# of their official duties. Pursuant to Title 17 Section 105 of the
# United States Code, this software is not subject to copyright
# protection within the United States. NIST assumes no responsibility
# whatsoever for its use by other parties, and makes no guarantees,
# expressed or implied, about its quality, reliability, or any other
# characteristic.
#
# We would appreciate acknowledgement if the software is used.

SHELL := /bin/bash

top_srcdir := $(shell cd .. ; pwd)

example_ttls := $(wildcard example-*.ttl)

validation_done_logs := $(foreach example_ttl,$(example_ttls),.$(example_ttl).validation.done.log)

all:

.example-%.validation.done.log: \
  example-% \
  $(top_srcdir)/.venv.done.log \
  $(top_srcdir)/ontology/generated-ontology.ttl \
  $(top_srcdir)/shapes/generated-shapes.ttl \
  sh-qc.ttl
	source $(top_srcdir)/venv/bin/activate \
	  && pyshacl \
	    --inference none \
	    --ont-graph $(top_srcdir)/ontology/generated-ontology.ttl \
	    --shacl sh-qc.ttl \
	    $<
	source $(top_srcdir)/venv/bin/activate \
	  && pyshacl \
	    --inference none \
	    --ont-graph $(top_srcdir)/ontology/generated-ontology.ttl \
	    --shacl $(top_srcdir)/shapes/generated-shapes.ttl \
	    $<
	touch $@

check: \
  $(validation_done_logs)

clean:
	@rm -f \
	  .*.done.log
