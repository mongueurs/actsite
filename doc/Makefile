# les fichiers sources
PODFILES = $(wildcard ../../act/doc/*.pod)

# les cibles finales
HTML = $(patsubst ../../act/doc/%.pod,%.html,$(PODFILES))

all: $(HTML)

# action !
%.html: ../../act/doc/%.pod
	(echo '[% TAGS <% %> %]' ; pom2 html $< ) | \
	grep -vE '<body|</body>' | \
	perl -0777 -pi -e 's|</pre>(\n+)<pre>|$$1|gi' \
	> $@
