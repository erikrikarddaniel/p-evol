DIFF = grep -v "^[ ]*$$" $@.out | diff $@.expect -

CHECK = if [ ` $(DIFF) | wc -l ` -eq 0 ]; then echo "*** $@ OK ***"; else echo "*** $@ FAILED ***"; echo "Here's a diff: "; $(DIFF); exit 1; fi

SIZE_CHECK = if [ ` stat -c "%s" $@.out ` -eq ` stat -c "%s" $@.expect ` ]; then echo "*** $@ OK ***"; else echo "*** $@ FAILED ($@.out and $@.expect different sizes) ***"; exit 1; fi

GREP_CHECK = pattern=`cat $@.expect`; if [ `grep "$$pattern" $@.out | wc -l` -gt 0 ]; then echo "*** $@ OK ***"; else echo "*** $@ FAILED ***"; echo "Didn't find $$pattern in output"; exit 1; fi

XML_CHECK =

all: grasim2matrix

clean:
	@rm -rf *.out *.tmp err 

grasim2matrix: grasim2matrix.00 grasim2matrix.01

grasim2matrix.00:
	@../../scripts/grasim2matrix --transform=minus --transformval=1 $@.sim > $@.out
	@$(CHECK)

grasim2matrix.01:
	@../../scripts/grasim2matrix --transform=inverse $@.sim > $@.out
	@$(CHECK)
