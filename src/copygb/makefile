# This makefile compiles copygb
# NOTE: This is a serial build as the code is written to be serial
# Usage: copygb [-g "grid [kgds]"] [-i "ip [ipopts]"] [-k "kpds"] [-v "uparms"]
#              [-B mapgrib [-b mapindex] [-A "<> mapthreshold"] [-K "mapkpds"]]
#              [-M "mask"/mergegrib [-m mergeindex]] [-X] [-a] [-N namelist]
#       then either:
#              grib1 index1 grib2
#            or:
#              -x grib1 grib2
#
# Perform destaggering (NMM) and HORIZONTAL interpolation to a defined output grid.
# Create output grid NOT fixed by model integration domain

SHELL    = /bin/sh
TARGET   = copygb.exe

#
# build configuration based on architecture and compiler
include ../../configure.upp

#
# directories of shared resources
LOCALINC = -I$(INCMOD)

LLIBDIR   = -L$(NCEPLIBS_DIR)/lib
NCEPLIBS  = -lip_d -lbacio_4 -lsp_v2.0.2_d -lw3nco_v2.0.6_4 -lw3emc_v2.2.0_4
LIBS     = $(LLIBDIR) $(NCEPLIBS)

#
# extra compilation/link flags
#   we are using single word (4 byte) for all libraries
EXTRA_FFLAGS   =
#EXTRA_FFLAGS   = -c -r8
EXTRA_LDFLAGS  = $(LIBS) 

SRCS=	copygb.f
OBJS=   $(SRCS:.f=.o)

#
# TARGETS

all: $(BINDIR)/$(TARGET)

$(BINDIR)/$(TARGET): $(TARGET)
	$(CP) $(TARGET) $(BINDIR)

$(TARGET): $(SRCS) kinds_mod.o
	$(SFC) -o $@ $(SRCS) kinds_mod.o $(FFLAGS) $(EXTRA_FFLAGS) $(LDFLAGS) $(EXTRA_LDFLAGS)

kinds_mod.o: kinds_mod.f
	$(F90)  -c $(FFLAGS) $(EXTRA_FFLAGS) $<

clean:	
	@ echo -e "\n <><><><> CLEAN <><><><>\n"
	$(RM) $(TARGET) $(OBJS)
	$(RM) $(BINDIR)/$(TARGET)

.IGNORE:
.PHONY: clean
