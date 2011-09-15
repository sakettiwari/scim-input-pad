## Makefile.am -- Process this file with automake to produce Makefile.in
## Copyright (C) 2002 James Su
##
## This program is free software; you can redistribute it and/or modify
## it under the terms of the GNU General Public License as published by
## the Free Software Foundation; either version 2, or (at your option)
## any later version.
##
## This program is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU General Public License for more details.
##
## You should have received a copy of the GNU General Public License
## along with this program; if not, write to the Free Software
## Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

MAINTAINERCLEANFILES	= Makefile.in

icondir			= $(SCIM_ICONDIR)
icon_DATA		= input-pad.png

bin_SCRIPTS		= scim-input-pad

srcdir = .
top_srcdir = ..
top_builddir = ..

INPUT_PAD_SOURCE_FILES	= base.pad.in	\
			  keyboard.pad.in	\
			  japanese.pad.in	\
			  chinese.pad,in	\
			  korean.pad.in		\
			  arabian.pad.in	\
			  ethiopic.pad.in	\
			  india_bengali.pad.in	\
			  india_chiki.pad.in	\
			  india_devanagari.pad.in	\
			  india_gujarati.pad.in		\
			  india_gurmukhi.pad.in	\
			  india_kannada.pad.in	\
			  india_lepcha.pad.in	\
			  india_limbu.pad.in	\
			  india_malayalam.pad.in	\
			  india_oriya.pad.in	\
			  india_saurashtra.pad.in	\
			  india_sinhala.pad.in	\
			  india_syloti_nagri.pad.in	\
			  india_tamil.pad.in	\
			  india_telugu.in	\
			  armenian.pad.in	\
			  balinese.pad.in	\
			  buginese.pad.in	\
			  cham.pad.in		\
			  georgian.pad.in	\
			  hebrew.pad.in		\
			  kaya.pad.in		\
			  khmer.pad.in		\
			  lao.pad.in		\
			  myanmar.pad.in	\
			  mongolian.pad.in	\
			  philipine_buhid.pad.in	\
			  philipine_hanunoo.pad.in	\
			  philipine_tagalog.pad.in	\
			  russian.pad.in	\
			  tai_lue.pad.in	\
			  rejang.pad.in		\
			  sundanese.pad.in	\
			  tai_le.pad.in		\
			  thai.pad.in		\
			  tibet.pad.in

scim_input_pad_datadir	= @SCIM_INPUT_PAD_DATADIR@
scim_input_pad_data_DATA= $(INPUT_PAD_DEST_FILES)

EXTRA_DIST		= input-pad.png $(INPUT_PAD_SOURCE_FILE)

CLEANFILES		= *.bak scim-input-pad $(INPUT_PAD_DEST_FILES)

*.pad:	*.pad.in	$(INTLTOOL_MERGE) $(top_srcdir)/po/*.po ; LC_ALL=C $(INTLTOOL_MERGE) -d -u -c $(top_builddir)/po/.intltool-merge-cache $(top_srcdir)/po $< ($)@'
