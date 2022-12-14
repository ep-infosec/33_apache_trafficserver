# Makefile.am for the src/records
#
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

include $(top_srcdir)/build/tidy.mk

check_PROGRAMS = test_librecords test_librecords_on_eventsystem

AM_CPPFLAGS += \
	-I$(abs_top_srcdir)/iocore/eventsystem \
	-I$(abs_top_srcdir)/iocore/utils \
	-I$(abs_top_srcdir)/mgmt \
	-I$(abs_top_srcdir)/mgmt/api/include \
	-I$(abs_top_srcdir)/mgmt/utils \
	-I$(abs_top_srcdir)/include \
	-I$(abs_top_srcdir)/lib \
	$(TS_INCLUDES)

noinst_LIBRARIES = librecords_lm.a librecords_p.a

librecords_COMMON = \
	I_RecAlarms.h \
	I_RecCore.h \
	I_RecDefs.h \
	I_RecEvents.h \
	I_RecHttp.h \
	I_RecMutex.h \
	I_RecSignals.h \
	P_RecCore.cc \
	P_RecCore.h \
	P_RecDefs.h \
	P_RecFile.h \
	P_RecMessage.h \
	P_RecUtils.h \
	RecConfigParse.cc \
	RecCore.cc \
	RecDebug.cc \
	RecFile.cc \
	RecHttp.cc \
	RecMessage.cc \
	RecMutex.cc \
	RecRawStats.cc \
	RecUtils.cc

librecords_lm_a_SOURCES = \
	$(librecords_COMMON) \
	I_RecLocal.h \
	P_RecLocal.h \
	RecLocal.cc

librecords_p_a_SOURCES = \
	$(librecords_COMMON) \
	I_RecProcess.h \
	P_RecProcess.h \
	RecProcess.cc

TESTS = $(check_PROGRAMS)

test_librecords_CPPFLAGS = $(AM_CPPFLAGS)\
	-I$(abs_top_srcdir)/tests/include

test_librecords_SOURCES = \
    unit_tests/unit_test_main.cc \
    unit_tests/test_RecHttp.cc

test_librecords_LDADD = \
	$(top_builddir)/src/records/librecords_p.a \
	$(top_builddir)/mgmt/libmgmt_p.la \
	$(top_builddir)/iocore/eventsystem/libinkevent.a \
	$(top_builddir)/src/tscpp/util/libtscpputil.la \
	$(top_builddir)/src/tscore/libtscore.la \
	$(top_builddir)/proxy/shared/libUglyLogStubs.a \
	@HWLOC_LIBS@ @LIBCAP@

test_librecords_on_eventsystem_CPPFLAGS = $(AM_CPPFLAGS)\
	-I$(abs_top_srcdir)/tests/include

test_librecords_on_eventsystem_SOURCES = \
    unit_tests/unit_test_main_on_eventsystem.cc \
	unit_tests/test_DynamicStats.cc

test_librecords_on_eventsystem_LDADD = \
	$(top_builddir)/src/records/librecords_p.a \
	$(top_builddir)/mgmt/libmgmt_p.la \
	$(top_builddir)/iocore/eventsystem/libinkevent.a \
	$(top_builddir)/src/tscpp/util/libtscpputil.la \
	$(top_builddir)/src/tscore/libtscore.la \
	$(top_builddir)/proxy/shared/libUglyLogStubs.a \
	@HWLOC_LIBS@ @LIBCAP@

clang-tidy-local: $(sort $(DIST_SOURCES))
	$(CXX_Clang_Tidy)
