MPP_LIB =  ../../mpp_charset.ml ../../mpp_charstream.ml ../../mpp_out.ml ../../mpp_stringmap.ml ../../mpp_actions.ml 
MPP_CMOs = $(addsuffix .cmo, $(basename $(MPP_LIB)))
MPP_CMXs = $(addsuffix .cmx, $(basename $(MPP_LIB)))

OCAMLC   = ocamlc -I ../../
OCAMLOPT = ocamlopt  -I ../../

all : ocamltohtml
ocamltohtml:ocamltohtml.opt
	cp $< $@

ocamltohtml.byte : ocamltohtml_lexer.cmo ocamltohtml_main.cmo
	$(OCAMLC) $(MPP_CMOs) $+ -o $@

ocamltohtml.opt : ocamltohtml_lexer.cmx ocamltohtml_main.cmx
	$(OCAMLOPT) $(MPP_CMXs) $+ -o $@

%.cmo:%.ml
	$(OCAMLC) -c $<

%.cmx:%.ml
	$(OCAMLOPT) -c $<

ocamltohtml_main.cmx:ocamltohtml_lexer.cmx
ocamltohtml_main.cmo:ocamltohtml_lexer.cmo

ocamltohtml_lexer.ml:ocamltohtml_lexer.mll
	ocamllex $<

clean:
	rm -f *~ *.cm[xoi]  *.o ocamltohtml ocamltohtml_lexer.ml


all2:
	ocamllex ocamltohtml_lexer.mll  && ocamlc ocamltohtml_lexer.ml && ocamlc ocamltohtml_lexer.cmo  ocamltohtml_main.ml -o ocamltohtml


ocamltohtml_all.ml:ocamltohtml_lexer.ml
	for i in ../../mpp_charset.ml ../../mpp_charstream.ml ../../mpp_out.ml ../../mpp_stringmap.ml ../../mpp_actions.ml  ocamltohtml_lexer.ml ; do echo module ; ocaml -stdin <<< "print_endline (String.capitalize Sys.argv.(1))" $$(basename $$i .ml) ; echo = struct ; cat $$i ; echo end ; done > ocamltohtml_all.ml ; cat ocamltohtml_main.ml >> ocamltohtml_all.ml

