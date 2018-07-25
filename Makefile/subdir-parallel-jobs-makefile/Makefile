#######################################################################
#����ĸ�Ŀ¼
PWD := $(shell pwd)
export ROOTDIR = $(dir $(PWD))
GUI_RESOLUTION ?= 480x854
export CONFIG_FILE ?= config_$(GUI_RESOLUTION).mk
include $(ROOTDIR)/cfg/$(CONFIG_FILE)

CPU_THREADS ?= $(shell grep -c ^processor /proc/cpuinfo)

SUBDIRS:=param  

ifeq ($(ENABLE_GUI_MENU),1)
SUBDIRS+=gui  
endif
ifeq ($(ENABLE_STREAM_BUF),1)
SUBDIRS+=streamBuf  
endif
ifeq ($(ENABLE_AV_CODEC),1)
SUBDIRS+=avCodec  
endif
ifeq ($(ENABLE_LOG),1)
SUBDIRS+=log  
endif
ifeq ($(ENABLE_RTSP),1)
SUBDIRS+=rtsp  
endif
ifeq ($(ENABLE_UVC_HOST),1)
SUBDIRS+=uvcHost  
endif
ifeq ($(ENABLE_MKV),1)
SUBDIRS+=mkv  
endif
ifeq ($(ENABLE_RECORDER),1)
SUBDIRS+=record  
endif

export ABS_SUBDIRS=$(addprefix $(PWD)/,$(SUBDIRS))
MAKEFLAGS +=--no-print-directory

.PHONY:all clean app $(SUBDIRS)

all:app
clean:app
app:$(SUBDIRS)	
	$(MAKE) -j$(CPU_THREADS) -C $@ $(MAKECMDGOALS) 
	
$(SUBDIRS):	
	$(MAKE) -j$(CPU_THREADS) -C $@ $(MAKECMDGOALS)
	
include $(ROOTDIR)/rule.mk


#######################################################################
