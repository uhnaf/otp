#
# %CopyrightBegin%
# 
# Copyright Ericsson AB 2006-2012. All Rights Reserved.
# 
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# 
# %CopyrightEnd%
#
#=============================================================================
#
#    File:  lib/typer/src/Makefile
# Authors:  Kostis Sagonas
#
#=============================================================================

include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Application version
# ----------------------------------------------------
include ../vsn.mk
VSN=$(TYPER_VSN)

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/lib/typer-$(VSN)

# ----------------------------------------------------
# Orientation information -- find dialyzer's dir
# ----------------------------------------------------
DIALYZER_DIR = $(ERL_TOP)/lib/dialyzer

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------
MODULES = typer

HRL_FILES=
ERL_FILES= $(MODULES:%=%.erl)
INSTALL_FILES= $(MODULES:%=$(EBIN)/%.$(EMULATOR)) $(APP_TARGET) $(APPUP_TARGET)
TARGET_FILES= $(INSTALL_FILES)

APP_FILE= typer.app
APP_SRC= $(APP_FILE).src
APP_TARGET= $(EBIN)/$(APP_FILE)

APPUP_FILE= typer.appup
APPUP_SRC= $(APPUP_FILE).src
APPUP_TARGET= $(EBIN)/$(APPUP_FILE)

# ----------------------------------------------------
# FLAGS
# ----------------------------------------------------
ERL_COMPILE_FLAGS += +warn_export_vars +warn_untyped_record +warn_missing_spec

# ----------------------------------------------------
# Targets
# ----------------------------------------------------

debug opt: $(TARGET_FILES)

docs:

clean:
	rm -f $(TARGET_FILES)
	rm -f core

# ----------------------------------------------------
# Special Build Targets
# ----------------------------------------------------

$(EBIN)/typer.$(EMULATOR): typer.erl ../vsn.mk Makefile
	$(erlc_verbose)erlc -W  $(ERL_COMPILE_FLAGS) -DVSN="\"v$(VSN)\"" -o$(EBIN) typer.erl

$(APP_TARGET): $(APP_SRC) ../vsn.mk
	$(vsn_verbose)sed -e 's;%VSN%;$(VSN);' $< > $@

$(APPUP_TARGET): $(APPUP_SRC) ../vsn.mk
	$(vsn_verbose)sed -e 's;%VSN%;$(VSN);' $< > $@

# ---------------------------------------------------------------------
# dependencies
# ---------------------------------------------------------------------


# ----------------------------------------------------
# Release Target
# ---------------------------------------------------- 
include $(ERL_TOP)/make/otp_release_targets.mk

release_spec: opt
	$(INSTALL_DIR) "$(RELSYSDIR)/src"
	$(INSTALL_DATA) $(ERL_FILES) $(HRL_FILES) $(YRL_FILES) \
		"$(RELSYSDIR)/src"
	$(INSTALL_DIR) "$(RELSYSDIR)/ebin"
	$(INSTALL_DATA) $(INSTALL_FILES) "$(RELSYSDIR)/ebin"

release_docs_spec:
