
.PHONY: clean
SOURCES = developer-manual.tex atex.tex

apireference:
#	Create the api reference using ROBODoc, requires full tree checkout
	robodoc --src ../../tapper/tapper-autoreport/ --doc ./content/apireference --rc robodoc.rc
#	Remove unnecessary \index from apireference
	sed -i -E 's|^.*index$$||g' content/apireference.tex

pdf: $(SOURCES) clean apireference
#	pdflatex -interaction=batchmode cvmfstech > /dev/null
	pdflatex -interaction=batchmode developer-manual	
	bibtex developer-manual
	makeindex developer-manual.idx
	pdflatex -interaction=batchmode developer-manual > /dev/null
	pdflatex -interaction=batchmode developer-manual | grep -i 'overful|underful' || true
	thumbpdf developer-manual
	pdflatex -interaction=batchmode developer-manual > /dev/null
	pdfopt developer-manual.pdf developer-manual.pdf.opt
	rm -f developer-manual.pdf
	mv developer-manual.pdf.opt developer-manual.pdf

clean: 
	rm -f developer-manual*.idx developer-manual*.log developer-manual*.toc cvmfs-blocks*.tex 
	rm -f developer-manual*.ilg developer-manual*.ind developer-manual*.tpt q*.log texput*.log cernlogo*.log developer-manual*.out
	rm -f developer-manual*.bbl developer-manual*.blg developer-manual*.lol
	rm -f content/protocol*.bbl content/protocol*.log content/protocol*.blg
	rm -f *.out
	find . -name "*.aux" -exec rm {} \;

