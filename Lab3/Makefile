#
# Created by gmakemake (Ubuntu Jul 25 2014) on Wed Feb 26 00:08:55 2020
#

#
# Definitions
#

.SUFFIXES:
.SUFFIXES:	.a .o .c .C .cpp .s .S
.c.o:
		$(COMPILE.c) $<
.C.o:
		$(COMPILE.cc) $<
.cpp.o:
		$(COMPILE.cc) $<
.S.s:
		$(CPP) -o $*.s $<
.s.o:
		$(COMPILE.cc) $<
.c.a:
		$(COMPILE.c) -o $% $<
		$(AR) $(ARFLAGS) $@ $%
		$(RM) $%
.C.a:
		$(COMPILE.cc) -o $% $<
		$(AR) $(ARFLAGS) $@ $%
		$(RM) $%
.cpp.a:
		$(COMPILE.cc) -o $% $<
		$(AR) $(ARFLAGS) $@ $%
		$(RM) $%

CC =		gcc
CXX =		g++

RM = rm -f
AR = ar
LINK.c = $(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS)
LINK.cc = $(CXX) $(CXXFLAGS) $(CPPFLAGS) $(LDFLAGS)
COMPILE.c = $(CC) $(CFLAGS) $(CPPFLAGS) -c
COMPILE.cc = $(CXX) $(CXXFLAGS) $(CPPFLAGS) -c
CPP = $(CPP) $(CPPFLAGS)
########## Flags from header.mak

#
# This header.mak file sets up all the necessary options for compiling
# and linking C and C++ programs which use OpenGL, GLFW, and/or GLEW on
# the CS Ubuntu systems.  To use it, place it in the same directory as
# your source code, and run the command
#
#	gmakemake > Makefile
#
# To compile and link your program, just run "make".
#

# locations of important directories if the header files
# and library files aren't in the standard places
INCLUDE =
LIBDIRS =

# common linker options
LDLIBS = -lGL -lm -lGLEW -lglfw

# language-specific linker options
CLDLIBS =
CCLDLIBS =

# compiler flags
CCFLAGS = -g $(INCLUDE) -DGL_GLEXT_PROTOTYPES
CFLAGS = -std=c99 $(CCFLAGS)
CXXFLAGS = $(CCFLAGS)

# linker flags
LIBFLAGS = -g $(LIBDIRS) $(LDLIBS)
CLIBFLAGS = $(LIBFLAGS) $(CLDLIBS)
CCLIBFLAGS = $(LIBFLAGS) $(CCLDLIBS)

########## End of flags from header.mak


CPP_FILES =	Buffers.cpp Canvas.cpp Clipper.cpp ShaderSetup.cpp clipMain.cpp
C_FILES =	
PS_FILES =	
S_FILES =	
H_FILES =	Buffers.h Canvas.h Clipper.h ShaderSetup.h Vertex.h
SOURCEFILES =	$(H_FILES) $(CPP_FILES) $(C_FILES) $(S_FILES)
.PRECIOUS:	$(SOURCEFILES)
OBJFILES =	Buffers.o Canvas.o Clipper.o ShaderSetup.o 

#
# Main targets
#

all:	clipMain 

clipMain:	clipMain.o $(OBJFILES)
	$(CXX) $(CXXFLAGS) -o clipMain clipMain.o $(OBJFILES) $(CCLIBFLAGS)

#
# Dependencies
#

Buffers.o:	Buffers.h Canvas.h
Canvas.o:	Canvas.h
Clipper.o:	Clipper.h Vertex.h
ShaderSetup.o:	ShaderSetup.h
clipMain.o:	Buffers.h Canvas.h Clipper.h ShaderSetup.h Vertex.h

#
# Housekeeping
#

Archive:	archive.tgz

archive.tgz:	$(SOURCEFILES) Makefile
	tar cf - $(SOURCEFILES) Makefile | gzip > archive.tgz

clean:
	-/bin/rm -f $(OBJFILES) clipMain.o core

realclean:        clean
	-/bin/rm -f clipMain 
