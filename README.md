# saf-documentation

This is upstream source code of [Service Assurance Framework](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/13/html/service_assurance_framework/index) documentation. All content in this repository uses [AsciiDoctor](https://asciidoctor.org/) syntax and aims to follow [Guidelines for Red Hat Documentation](https://redhat-documentation.github.io/). This is a **work in progress*.

## Building

Install required tools. In Fedora perform:

    dnf -y install ruby asciidoctor asciidoctor-pdf make

In MacOS required tools can be installed via brew but instead "make" call "gmake":

    brew install asciidoctor make

Alternatively, XCode development environment can be installed to have make utility available on PATH, however this takes about an hour to download and install and requires several gigabytes of HDD space:

	xcode-select --install

If AsciiDoctor is not available in repositories or under RVM/rbenv, simply install it from rubygems:

  	gem install asciidoctor asciidoctor-pdf --pre

Then simply run `make` or `make html` which builds HTML artifacts. Generating PDF output is slow, therefore command `make pdf` must be used separately. To make both formats in one command, use `make html pdf`. To build downstream version perform `make BUILD=satellite`.

Few additional make targets are available on the guide level. To quickly build HTML version and open new tab in a browser do:

    cd doc-Service-Assurance-Framework
    make browser

Similarly, to build and open PDF version do:

    make open-pdf

The final artifacts can be found in the ./build subdirectory. Note that GNU Makefile tracks changes and only builds relevant artifacts, to trigger full rebuild use `make clean` to delete build directory and start over.

## Reading or Publishing

We do not publish the content yet to prevent users confusion, however this section will cover steps required to publish the content. We should make sure that only the last stable version of the HTML document is indexed by search engines, old and nightly builds should not be indexed. All PDFs should be available for download though.

## Contributing

Please read [Guidelines for Red Hat Documentation](https://redhat-documentation.github.io/) before opening a Pull Request. Additional rules apply:

Never write "Service Assurance Framework" or "SAF" words directly but use the following variables:

| Variable | Upstream value | Downstream value |
| -------- | -------------- | ---------------- |


Variables cannot be used in shell or code examples. To use them, use "attributes" keyword:

	[options="nowrap" subs="+quotes,+attributes"]
	----
	# ls {VariableName}
	----

Hide or show specific blocks, paragraphs, warnings or chapters via special variable called "build". Its value can be set either to "foreman" or "satellite":

	ifeval::["{build}" == "upstream"]
	NOTE: This part is only relevant for deployments with Katello plugin.
	endif::[]

When doing review, consider checking out the topic branch and putting necessary changes on top of author's work to making many comments on github.

We should avoid using phases like, "Starting from version 6.5 or 1.22" because it is not possible to easily translate these strings in both the streams.

## The process (TODO)

This is what we are working on right now:

* [x] Initial import of Service Assurance Framework Guide
* [x] Provide Makefiles
