
HOME := $(shell echo ${GSF_HOME})
CC := $(shell echo ${GSF_CC})
AR := $(shell echo ${GSF_AR})
CFLAGS := $(shell echo ${GSF_CFLAGS})
LDFLAGS := -g $(shell echo ${GSF_LDFLAGS})
TARG := bin/app.exe

#============================================================= 

INCS := -I$(HOME) -Isrc -Iinc \
        -I$(HOME)/fw/comm/inc 
        
#SRCS := $(shell ls src/*.c)
SRCS := $(shell find src -type f -name "*.c" -o -name "*.cpp")
OBJS := $(patsubst %.c, %.o, $(SRCS))

LIBS += -L$(HOME)/lib/$(GSF_CPU_ARCH) -Llittlevgl -llittlevgl -llvgl -lcomm -lcfifo -lrt -lnm -lcjson -lm -lpthread

$(TARG): SJB $(OBJS)
	@$(MAKE) -C littlevgl || exit "$$?"
	$(CC) $(LDFLAGS) -o $@ $(OBJS) $(LIBS)
	cp $(TARG) $(HOME)/bin/$(GSF_CPU_ARCH)/ -v

.c.o:
	$(CC) $(CFLAGS) -c $< $(INCS) -o $@

SJB:
	touch src/sjb_app.c;touch src/cfg.c
  
.Phony: clean
clean:
	$(MAKE) -C littlevgl clean
	-rm $(TARG) $(OBJS) src/*.bak -rf
