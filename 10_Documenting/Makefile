# xgettext --keyword=_ --language=C --add-comments --sort-output -o po/number_diviner.pot number_diviner.c
# msginit --input=po/number_diviner.pot --locale=ru --output=po/number_diviner_ru.po
# msgfmt --output-file=number_diviner.mo po/number_diviner_ru.po

CC = gcc

TGT_NAME = number_diviner

all: $(TGT_NAME) ru/LC_MESSAGES/$(TGT_NAME).mo man DoxygenOut

%.o : %.c
	$(CC) -c $< -o $@

$(TGT_NAME): $(TGT_NAME).o roman.o
	$(CC) $^ -o $@

%/LC_MESSAGES/$(TGT_NAME).mo: po/$(TGT_NAME).%.po
	mkdir -p `dirname $@`
	msgfmt $< -o $@

po/$(TGT_NAME).%.po: po/$(TGT_NAME).pot
	msgmerge -U $@ $<

po/$(TGT_NAME).pot: $(TGT_NAME).c
	xgettext -k_ -c $(TGT_NAME).c -o update.pot
	msgmerge -U $@ update.pot

man: man1/$(TGT_NAME).1

man1/$(TGT_NAME).1: $(TGT_NAME)
	mkdir -p man1
	help2man ./$(TGT_NAME) > $@

DoxygenOut:
	doxygen DoxyFile

.PHONY: show_man
show_man: man
	MANPATH=`pwd` man $(TGT_NAME)


.PHONY: clean
clean:
	rm -rf DoxygenOut
	rm -rf man1
	rm -f $(TGT_NAME)
	rm -f *.o
	rm -f po/*.pot~ po/*.po~ update.pot
	rm -rf */LC_MESSAGES/*
	rm -rf ru/