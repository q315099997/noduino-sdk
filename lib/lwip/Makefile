
#############################################################
# Required variables for each makefile
# Discard this section from all parent makefiles
# Expected variables (with automatic defaults):
#   CSRCS (all "C" files in the dir)
#   SUBDIRS (all subdirs with a Makefile)
#   GEN_LIBS - list of libs to be generated ()
#   GEN_IMAGES - list of images to be generated ()
#   COMPONENTS_xxx - a list of libs/objs in the form
#     subdir/lib to be extracted and rolled up into
#     a generated lib/image xxx.a ()
#
ifndef PDIR
UP_EXTRACT_DIR = ..
GEN_LIBS = liblwip.a
COMPONENTS_liblwip = api/liblwipapi.a	\
						app/liblwipapp.a	\
						core/liblwipcore.a	\
						core/ipv4/liblwipipv4.a	\
						netif/liblwipnetif.a
endif

# noduino sdk base dir
SDK_BASE := ../..

#############################################################
# Configuration i.e. compile options etc.
# Target specific stuff (defines etc.) goes in here!
# Generally values applying to a tree are captured in the
#   makefile at its root level - these are then overridden
#   for a subtree within the makefile rooted therein
#
DEFINES += -DICACHE_FLASH

#############################################################
# Recursion Magic - Don't touch this!!
#
# Each subtree potentially has an include directory
#   corresponding to the common APIs applicable to modules
#   rooted at that subtree. Accordingly, the INCLUDE PATH
#   of a module can only contain the include directories up
#   its parent path, and not its siblings
#
# Required for each makefile to inherit from the parent
#

INCLUDES := $(INCLUDES) -I $(PDIR)include
INCLUDES += -I $(SDK_BASE)/include -I ./
PDIR := $(SDK_BASE)/sdk/$(PDIR)
sinclude $(PDIR)/Makefile

LIB_INCDIR	:= ../../include/mqtt

install: all
	mv .output/lib/*.a ../ 
	rm -rf $(LIB_INCDIR)
	mkdir -p $(LIB_INCDIR)
	cp -a include/* $(LIB_INCDIR)/