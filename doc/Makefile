# this Makefile assumes that the act/ and actsite/ working directories
# were checked out in the same subdirectory

# source pod files
PODFILES = $(wildcard ../../act/doc/*.pod)

# target html files
HTML = todo.html $(patsubst ../../act/doc/%.pod,%.html,$(PODFILES))

all: svnup $(HTML)

# action !
%.html: ../../act/doc/%.pod
	(echo '[% TAGS <% %> %]' ; pom2 html $< ) | \
	grep -vE '<body|</body>' | \
	perl -0777 -pi -e 's|</pre>(\n+)<pre>|$$1|gi' \
	> $@

todo.html: ../../act/TODO
	perl -0777ne 's/\A(.*)/=head1 $$1\n\n=over 4/;s/^([^=*\s]+.*)$$/=back\n\n=head2 $$1\n\n=over 4/gm;s{^\*( *)(.*?)^$$}{my($$i,$$s)=($$1,$$2);$$s=~s/^ $$i//g;"=item *\n\n$$s"}gems;print "[% TAGS <% %> %]\n\n$$_\n=back\n"' $< | \
	pom2 html - | \
	grep -vE '<body|</body>' | \
	perl -0777 -pi -e 's|</pre>(\n+)<pre>|$$1|gi' \
    > $@

svnup:
	pushd ../../act/doc ; svn up -q ; popd
