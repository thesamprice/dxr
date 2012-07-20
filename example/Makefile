export CC = clang++
export LD = ld


INCPATH	=	-I.

export CLANG_PLUGINS = -Xclang -load -Xclang $(DXRSRC)/xref-tools/cxx-clang/libclang-index-plugin.so -Xclang -add-plugin -Xclang dxr-index -Xclang -plugin-arg-dxr-index -Xclang .
export CFLAGS	     = $(CLANG_PLUGINS)
CFLAGS += -g2 -O2 

SRC = $(wildcard ./*.cpp)
HEADERS = $(wildcard ./*.h)

OBJ = $(CSRC:.c=.o)
OBJ += $(SRC:.cpp=.o)
OBJ += $(SSRC:.S=.o)

example  : $(HEADERS) $(OBJ) 
	$(CC) $(OBJ) -o $@ $(LIBS) $(GCOVFLAGS) $(GPROFFLAGS)
 	
%.d: %.o
	@$(OBJD) $< -D > $@

%.o: %.cpp $(HEADERS)
	@$(CC) -c $(CFLAGS) $(INCPATH) $< -o $@
	@echo Compiling $<

%.o: %.c $(HEADERS)
	@$(CC) -c $(CFLAGS) $(INCPATH) $< -o $@
	@echo Compiling $<

%.i: %.S $(HEADERS)
	@$(CC) $(PREFLAGS) $(INCPATH) $< -o $@
	@echo Preprocessing $<
	
%.o: %.i $(HEADERS)
	@$(ASM) $(ASMFLAGS) $(INCPATH) $< -o $@
	@echo Compiling $<

clean:
	$(RM) -v ./*.o
	$(RM) -v ./*.gcno
	$(RM) -v ./*.gch
	$(RM) -v ./*.gcda
	$(RM) -v ./*.sql
	$(RM) -v ./db/*.sql
	$(RM) -v ./db/*.log
	$(RM) -v ./db/db
	$(RM) -v ./gmon.out
	$(RM) -v ./example
