# Copyright (C) 2018  Dridi Boukelmoune
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

ACLOCAL_AMFLAGS = -I m4

include lcov.am
include rpm.am

# Configuration

nobase_nodist_noinst_SCRIPTS = \
	gcov-tool.sh \
	test/run.sh

CONFIG_SUFFIXES = .sh.in .sh

.sh.in.sh:
	@mkdir -p test
	$(AM_V_GEN) $(SED) \
		-e 's:[@]builddir[@]:$(abs_top_builddir):' \
		-e 's:[@]GCOV[@]:$(GCOV):' \
		<'$<' >$@
	chmod +x $@

# Binaries

lib_LTLIBRARIES = libbjxa.la
bin_PROGRAMS = bjxa
include_HEADERS = bjxa.h

bjxa_LDADD = libbjxa.la

# Packaging

pkgconfigdir = $(libdir)/pkgconfig

dist_pkgconfig_DATA = bjxa.pc

# Documentation

dist_doc_DATA = README.rst
dist_man_MANS = bjxa.1 bjxa.3

if DOCS
DOCS_SUFFIXES = .1 .3 .1.rst .3.rst

.1.rst.1:
	$(AM_V_GEN) $(RST2MAN) $< $@

.3.rst.3:
	$(AM_V_GEN) $(RST2MAN) $< $@
endif

# Test suite

LOG_COMPILER = ./test/run.sh

TESTS = \
	test/test_dummy.sh

# Distribution

SUFFIXES = $(CONFIG_SUFFIXES) $(DOCS_SUFFIXES)

DISTCHECK_CONFIGURE_FLAGS = --disable-docs
DISTCLEANFILES = $(nobase_nodist_noinst_SCRIPTS)

EXTRA_DIST = \
	$(TESTS) \
	bjxa.1.rst \
	bjxa.3.rst \
	bjxa.spec \
	gcov-tool.sh.in \
	test/run.sh.in