# this Makefile assumes that the act/ and actsite/ working directories
# were checked out in the same subdirectory

# source pod files
PODFILES = $(wildcard ../../act/doc/*.pod)

# target html files
HTML = $(patsubst ../../act/doc/%.pod,%.html,$(PODFILES))

all: svnup $(HTML)

# action !
%.html: ../../act/doc/%.pod
	(echo '[% TAGS <% %> %]' ; pom2 html $< ) | \
	grep -vE '<body|</body>' | \
	perl -0777 -pi -e 's|</pre>(\n+)<pre>|$$1|gi' \
	> $@

svnup:
	pushd ../../act/doc ; svn up -q ; popd
