TARGET= main
TARGET_TIKZ=tikz
FOLDER_TIKZ=tikz_figs
# make pdf by default
all: ${TARGET}.pdf

# it doesn't really need the .dvi, but this way all the refs are right
%.pdf : %.dvi 
	latex ${TARGET}.tex
	latex ${TARGET}.tex
	latex ${TARGET}.tex
	dvipdfmx ${TARGET}.dvi

${TARGET}.bbl: ./humanawarenav.bib
# in case we don't already have a .aux file listing citations
# this should probably be a separate makefile target/dependency instead
# of doing it every time... but *shrug*
	latex ${TARGET}.tex
# get the citations out of the bibliography
	bibtex ${TARGET}
# do it again in case there are out-of-order cross-references
	latex ${TARGET}.tex

${TARGET}.dvi: ${TARGET}.bbl ${TARGET}.tex
	latex ${TARGET}.tex

#shortcut, so we can say "make ps"
ps: ${TARGET}.ps

${TARGET}.ps: ${TARGET}.dvi
	dvips -t a4 ${TARGET}.dvi

alldoc:
	make figures
	make all

#Compiles all the tikz pictures
figures: 
	latex -shell-escape -enable-write18 ${TARGET_TIKZ}.tex 
	make -f ${TARGET_TIKZ}.makefile
	rm -f ${TARGET_TIKZ}.aux
	rm -f ${TARGET_TIKZ}.dvi
	rm -f ${TARGET_TIKZ}.log
	rm -f ${TARGET_TIKZ}.pdf
#Compile only a figure make figure a=NAME_FIG
figure:
	latex -shell-escape -enable-write18 ${TARGET_TIKZ}.tex 
	make -f ${TARGET_TIKZ}.makefile ${FOLDER_TIKZ}/$a.epsi
	rm -f ${TARGET_TIKZ}.aux
	rm -f ${TARGET_TIKZ}.dvi
	rm -f ${TARGET_TIKZ}.log
	rm -f ${TARGET_TIKZ}.pdf

clean:
	rm -f ${TARGET}.log
	rm -f ${TARGET}.aux
	rm -f ${TARGET}.ps
	rm -f ${TARGET}.dvi
	rm -f ${TARGET}.bbl
	rm -f ${TARGET}.blg
	rm -f ${TARGET}.toc
	rm -f ${TARGET}.out
	rm -f ${TARGET}.pdf

cleanfigs:
	rm -f ${FOLDER_TIKZ}/*.eps
	rm -f ${FOLDER_TIKZ}/*.dpth
	rm -f ${FOLDER_TIKZ}/*.dep
	rm -f ${FOLDER_TIKZ}/*.log

cleanfig:
	rm -f ${FOLDER_TIKZ}/$a.eps
	rm -f ${FOLDER_TIKZ}/$a.dpth
	rm -f ${FOLDER_TIKZ}/$a.dep
	rm -f ${FOLDER_TIKZ}/$a.log

cleanallfigs:
	rm -f ${TARGET_TIKZ}.figlist
	rm -f ${TARGET_TIKZ}.makefile
	rm -f ${FOLDER_TIKZ}/*.eps
	rm -f ${FOLDER_TIKZ}/*.dpth
	rm -f ${FOLDER_TIKZ}/*.dep
	rm -f ${FOLDER_TIKZ}/*.log

cleanall:
	rm -f ${TARGET}.log
	rm -f ${TARGET}.aux
	rm -f ${TARGET}.ps
	rm -f ${TARGET}.dvi
	rm -f ${TARGET}.bbl
	rm -f ${TARGET}.blg
	rm -f ${TARGET}.toc
	rm -f ${TARGET}.out
	rm -f ${TARGET}.pdf
	rm -f ${TARGET_TIKZ}.aux
	rm -f ${TARGET_TIKZ}.dvi
	rm -f ${TARGET_TIKZ}.figlist
	rm -f ${TARGET_TIKZ}.log
	rm -f ${TARGET_TIKZ}.makefile
	rm -f ${TARGET_TIKZ}.out
	rm -f ${TARGET_TIKZ}.pdf
	rm -f tikz_figs/*.eps
	rm -f tikz_figs/*.dpth
	rm -f tikz_figs/*.dep
	rm -f tikz_figs/*.log


reallyclean: cleanall
	rm -f ${TARGET}.{ps,pdf}


#PHONY : ps all clean reallyclean
